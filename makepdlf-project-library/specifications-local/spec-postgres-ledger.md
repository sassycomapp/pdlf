---
title: "spec-postgres-ledger"
doc-id: "mb-dcf9c65e"
updated: "2026-10-09"
---
# PDLF Postgres Ledger Specification

**Purpose:** This file is the single source of truth for the PDLF Postgres ledger — the database schema, role, connection method, and operating principles. Based on ADR `[[postgres-ledger-replaces-flat-files]]`.

**Status:** Binding specification.

**Date:** 2026-07-13

---

## Connection

| Setting | Value |
|---|---|
| Host | `localhost` |
| Port | `5433` |
| Database | `pdlf` |
| Role | `pdlf_agent` |
| Password | `PGPASSWORD` in `.env` |
| Installation | `C:\Program Files\PostgreSQL\15\` (Windows) |
| WSL bridge | `powershell.exe -Command '$env:PGPASSWORD="..."; & "C:\Program Files\PostgreSQL\15\bin\psql.exe" -h localhost -p 5433 -U pdlf_agent -d pdlf -c "..."'` |

PostgreSQL (the ledger) runs on Windows. OpenCode runs in WSL. There are **two independent
reasons** the direct route is forbidden:

1. **WSL's binfmt does not pass Linux env vars to Windows executables** — an exported
   `PGPASSWORD` never reaches `psql.exe`.
2. **`localhost:5432` is the wrong server from both sides.** Inside WSL it is a completely
   different PostgreSQL cluster — WSL's own native PostgreSQL 16, hosting GBrain's `gbrain`
   database, not the PDLF ledger. On the Windows side, port 5432 is WSL's localhost relay
   to that same Instance B. A bare `psql` call without the bridge (from WSL) or without
   `-p 5433` (from Windows) does not fail visibly: it **silently connects to the wrong
   server**.

Always use the PowerShell bridge pattern with `-p 5433`. It executes on the Windows side,
where `localhost:5433` is the ledger cluster.

### Direct Windows PowerShell connection (human-run, not via OpenCode)

Confirmed live, 2026-08-26. A separate, valid connection pattern for a
developer running commands directly in Windows PowerShell, not through
OpenCode/WSL:

```powershell
$env:PGPASSWORD = "<value from .env>"
& "C:\Program Files\PostgreSQL\15\bin\psql.exe" -U pdlf_agent -d pdlf -h 127.0.0.1 -p 5433 -c "<SQL>"
```

One confirmed pitfall:

- **Do not build a `.sql` file via PowerShell's `Out-File` and pass it
  with `psql -f`.** `Out-File -Encoding utf8` adds a byte-order-mark
  invisible in the terminal, which `psql` fails to parse, producing
  `syntax error at or near "ï»¿ALTER"` on the first statement only. Pass
  SQL directly via `-c` instead, or verify the file is BOM-free before
  using `-f`.

Note: an earlier version of this document incorrectly attributed a
connection failure to `-h localhost` resolving to the IPv6 loopback
(`::1`) rather than IPv4. Live reproduction (2026-08-26, four-test
matrix: `localhost`/`127.0.0.1`/`::1`, each with correct and incorrect
password) confirmed the address was never the cause — `localhost` with
the correct password succeeds. The original failure was a wrong
password, not an address issue. Corrected here; either host form is
fine as long as the real value of `PGPASSWORD` from `.env` is used.

---

## Schema

**Corrected 2026-09-05 — this section was rewritten against the live database** (psql
`\d+` on every table, role `pdlf_agent`, Windows PostgreSQL 15.14). The previous version
documented an early schema and had drifted from reality for six of the seven tables.
`triage_findings` already matched and is confirmed unchanged.

Seven tables in schema `public`, owned by `pdlf_agent`, referentially enforced:

### `projects`

| Column | Type | Nullable | Default | Notes |
|---|---|---|---|---|
| `slug` | text | NO | — | Primary key. Project identifier (e.g., `mb5pdlf`) |
| `project_name` | text | NO | — | Human-readable name |
| `mode` | text | NO | — | `full` or `test` (CHECK `projects_mode_check`) |
| `library_path` | text | YES | — | Path to the project's project-library repo |
| `code_path` | text | YES | — | Path to the project's Anvil-connected code repo |
| `anvil_slug` | text | YES | — | Anvil app slug |
| `gbrain_source_docs` | text | YES | — | GBrain source ID for the project-library repo |
| `gbrain_source_code` | text | YES | — | GBrain source ID for the code repo |
| `is_active` | boolean | NO | `true` | Whether project is currently active |
| `created_at` | timestamptz | NO | `now()` | When the project row was created |

Primary key: `slug`. Referenced by `steps`, `gates`, `deviations`, `bft_records`, and
`isc` (all via `project_slug`).

### `steps`

| Column | Type | Nullable | Default | Notes |
|---|---|---|---|---|
| `id` | integer (serial) | NO | sequence | Primary key. Target of FKs from `gates`, `deviations`, `bft_records`, `triage_findings` |
| `project_slug` | text | NO | — | FK → `projects(slug)` |
| `step_number` | text | NO | — | Step number (11–46, plus lettered sub-steps). **Text, not integer** — text supports lettered sub-steps (e.g. `35A`) |
| `sort_order` | numeric | NO | — | Numeric ordering value for the step |
| `phase` | text | YES | — | Phase label |
| `step_type` | text | NO | — | `skill`, `manual`, `optional`, or `gate` (CHECK; lowercase values) |
| `skill_family` | text | YES | — | `gstack`, `matt-skills`, `opencode`, `manual`, or NULL (CHECK) |
| `skill_name` | text | YES | — | The invoked skill |
| `inputs_used` | jsonb | YES | — | Input artifacts/steps consumed by this step |
| `artifact_path` | text | YES | — | Path to step output artifact |
| `synthesized` | boolean | NO | `false` | Whether content was synthesized in test mode. **A separate boolean — not a status value** |
| `status` | text | NO | `'pending'` | `pending`, `in_progress`, `complete`, `blocked`, `skipped` (CHECK) |
| `next_action` | text | YES | — | Agent-facing guidance for next step |
| `started_at` | timestamptz | YES | — | When execution started |
| `completed_at` | timestamptz | YES | — | When execution completed |
| `blockers` | text | YES | — | Open blocker description |
| `notes_for_next_session` | text | YES | — | Carry-over notes for the next session |
| `gbrain_query` | text | YES | — | The GBrain query fired at substep 1 |
| `gbrain_results` | text | YES | — | Summary of the query results |

UNIQUE constraint: (`project_slug`, `step_number`). The only foreign key on `steps` is
`project_slug` — there is no inter-step constraint (see Principle 2).

### `gates`

| Column | Type | Nullable | Default | Notes |
|---|---|---|---|---|
| `id` | integer (serial) | NO | sequence | Primary key |
| `project_slug` | text | NO | — | FK → `projects(slug)` |
| `step_id` | integer | YES | — | FK → `steps(id)`. The step the gate follows |
| `gate_name` | text | NO | — | Gate identifier (e.g., `domain-locked`) |
| `passed` | boolean | NO | `false` | Whether gate was approved |
| `approved_at` | timestamptz | YES | — | When developer approved |
| `notes` | text | YES | — | Free-text gate notes |

### `deviations`

| Column | Type | Nullable | Default | Notes |
|---|---|---|---|---|
| `id` | integer (serial) | NO | sequence | Primary key |
| `project_slug` | text | NO | — | FK → `projects(slug)` |
| `step_id` | integer | YES | — | FK → `steps(id)`. The step the deviation belongs to |
| `description` | text | NO | — | Why the deviation was needed |
| `options_presented` | jsonb | YES | — | Three options presented to developer |
| `decision` | text | YES | — | Developer's chosen option |
| `decided_at` | timestamptz | YES | — | When the decision was made |

### `bft_records`

| Column | Type | Nullable | Default | Notes |
|---|---|---|---|---|
| `id` | integer (serial) | NO | sequence | Primary key |
| `project_slug` | text | NO | — | FK → `projects(slug)` |
| `step_id` | integer | YES | — | FK → `steps(id)` |
| `gate_id` | integer | YES | — | FK → `gates(id)` |
| `level` | text | NO | — | `full`, `light`, or `none` (CHECK) |
| `bones` | text | YES | — | Structure question answer |
| `muscle` | text | YES | — | Action question answer |
| `nerves` | text | YES | — | Information question answer |
| `fat` | text | YES | — | Filler question answer |
| `skin` | text | YES | — | Appearance question answer |
| `health` | text | YES | — | Health question answer |
| `recorded_at` | timestamptz | NO | `now()` | When the checkpoint was recorded |

### `isc` (Ideal State Criteria)

| Column | Type | Nullable | Default | Notes |
|---|---|---|---|---|
| `id` | integer (serial) | NO | sequence | Primary key |
| `project_slug` | text | NO | — | FK → `projects(slug)` |
| `isc_number` | text | NO | — | Criterion identifier (from ISA). **Text, not integer** |
| `description` | text | NO | — | What the criterion checks |
| `verify_method` | text | YES | — | How the criterion is verified |
| `status` | text | NO | `'pending'` | `pending`, `verified`, or `failed` (CHECK — `verified`, not `passed`) |
| `evidence` | text | YES | — | Verification evidence |
| `updated_at` | timestamptz | NO | `now()` | When the criterion row was last updated |

UNIQUE constraint: (`project_slug`, `isc_number`).

### `triage_findings`

**Corrected 2026-08-26 — the version below was stale against the live
schema.** Eight columns were added and the `source_step` constraint was
widened, both confirmed live against the running database, in support of a
security-review layer for PDLF (design work done outside this project's
own file tree at time of writing — not yet saved to a real path here).

**Confirmed 2026-09-05 — re-verified live (`\d+`); this table's columns are
unchanged since the 2026-08-26 correction.** One constraint value was
missing from this spec: the `triage_label` CHECK also allows `clear`
(six allowed values, not five).

| Column | Type | Notes |
|---|---|---|
| `id` | serial | Primary key |
| `step_id` | integer | FK → `steps(id)`. Identifies which feature-cycle execution this finding belongs to. |
| `finding_id` | text | Stable identifier from Steps 37-38 findings. No companion table — confirmed against the full seven-table schema list; free-standing identifier. |
| `source_step` | text | Which step produced this finding: `16, 17, 19, 20, 21, 34, 35, 36, 37, 38, 39, 45, 46` — widened from the original `36, 37, 38` to support Sentinel-originated findings from earlier steps |
| `triage_label` | text | One of: `needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`, `clear` (CHECK includes all six) |
| `resolution_note` | text | How the finding was resolved (developer-provided) |
| `resolved_by` | text | Who resolved it |
| `resolved_at` | timestamptz | When it was resolved |
| `created_at` | timestamptz | When the row was first written |
| `concern` | text | What the security concern is |
| `asset` | text | What data or capability is at risk |
| `threat` | text | Who or what could exploit it |
| `evidence` | text | Why this was flagged |
| `severity` | text | `Low`, `Medium`, `High`, `Critical` |
| `confidence` | text | `Low`, `Medium`, `High` |
| `recommended_control` | text | Proposed fix |
| `verification` | text | How to confirm it's resolved |

The `build-verified` gate queries this table: every row for the feature's `step_id` must have `triage_label = 'wontfix'` OR `resolved_at IS NOT NULL`. No open findings remain. The `.scratch/` triage output is transient input — the ledger row is authoritative.

---

## Principles

1. **The ledger is the single source of truth.** If it's not in `pdlf`, it didn't happen.
   Note, stated plainly: as of 2026-09-05 all seven tables are **empty** — zero rows in
   every table. This is expected, not a fault: PDLF's build has not yet reached real
   orchestrator use, and the 2026-07-19 self-test rows were cleaned up after that run.
   The principle describes how the ledger will operate once PDLF runs projects; it does
   not describe data that is present today.
2. **Step sequencing is enforced by the orchestrator, not the database.** Confirmed by
   live test 2026-07-18: the only foreign key on `steps` is `project_slug → projects(slug)`.
   There is no inter-step constraint — inserting Step 19 with no Step 16 present succeeds
   at the schema level. Step dependencies vary per step (see `[[run-plan]]`'s Step
   Dependencies table) and cannot be expressed as a fixed column-level FK. OpenCode checks
   `[[run-plan]]`'s dependency table before writing a step's ledger row; this is the actual
   enforcement point. A database-level trigger was considered and rejected: it would
   require a second, hand-maintained copy of the dependency graph already defined in
   `[[run-plan]]`, with no mechanism forcing the two to stay in sync — the same
   duplicate-source-of-truth failure found and corrected repeatedly elsewhere in this
   document set. The only writer with legitimate access to this database is OpenCode,
   operating through a PDLF step (see `AGENTS.md`); a raw write bypassing the orchestrator
   is already a policy violation before it reaches the schema.
3. **Step Receipts are generated from ledger rows.** The receipt IS the ledger row, formatted for reading — not a separately composed summary.
4. **No flat files.** Flat-file state management (state file, devlog, completion report) is fully retired.
5. **No narrative gloss can diverge from what actually happened.** The receipt is a snapshot of the row at the time it was written.
