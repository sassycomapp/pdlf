---
title: "spec-postgres-ledger"
doc-id: "mb-dcf9c65e"
updated: "2026-10-29"
---
# PDLF Postgres Ledger Specification

**Purpose:** This file is the single source of truth for the PDLF Postgres ledger — the database schema, role, connection method, and operating principles. Based on ADR `[[postgres-ledger]]`.

**Status:** Binding specification.


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

A separate connection pattern for a
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

Either `localhost` or `127.0.0.1` works as the host.

---

## Schema

Seven tables in schema `public`, owned by `pdlf_agent`, referentially enforced:

### `projects`

| Column | Type | Nullable | Default | Notes |
|---|---|---|---|---|
| `slug` | text | NO | — | Primary key. The business slug, hyphens kept (e.g., `mb-3-cs`) |
| `project_name` | text | NO | — | Human-readable name |
| `mode` | text | NO | — | `full` or `test` (CHECK `projects_mode_check`) |
| `library_path` | text | YES | — | Path to the project's project-library repo |
| `gbrain_source_docs` | text | YES | — | GBrain source ID for the project library (`{slug}-project-library`) |
| `app1_path`, `app2_path`, `app3_path`, `app5_path` | text | YES | — | Local path of each app's code repository (`C:\dev\dev-{slug}\{slug}-app{n}`). App 4 lives on the client's own Anvil account and has no path |
| `app1_address`, `app2_address`, `app3_address`, `app5_address` | text | YES | — | Each app's Anvil address. App 2's is recorded at release |
| `is_active` | boolean | NO | `true` | Whether project is currently active |
| `created_at` | timestamptz | NO | `now()` | When the project row was created |

Primary key: `slug`. Referenced by `steps`, `gates`, `deviations`, `bft_records`, and
`isc` (all via `project_slug`).

### `steps`

| Column | Type | Nullable | Default | Notes |
|---|---|---|---|---|
| `id` | integer (serial) | NO | sequence | Primary key. Target of FKs from `gates`, `deviations`, `bft_records`, `triage_findings` |
| `project_slug` | text | NO | — | FK → `projects(slug)` |
| `step_number` | text | NO | — | Step number: `02` to `10` for an entry point, `11` to `46` for a pipeline step, plus lettered sub-steps. **Text, not integer** — text supports lettered sub-steps (e.g. `35A`) |
| `sort_order` | numeric | NO | — | Numeric ordering value for the step |
| `phase` | text | YES | — | Phase label |
| `run` | text | NO | — | `app{n}` for the whole application (`app1`, `app2`, `app3` or `app5`, matching `app_number`), or the feature's short name for a feature or an update |
| `app_number` | smallint | NO | `1` | The app the row concerns: 1, 2, 3 or 5 (CHECK) |
| `step_type` | text | NO | — | `skill`, `manual`, `optional`, or `gate` (CHECK; lowercase values) |
| `skill_family` | text | YES | — | `gstack`, `matt-skills`, `opencode`, `manual`, `anvil`, `mybizz` (Sentinel and the mybizz-os skills), `security`, or NULL (CHECK) |
| `skill_name` | text | YES | — | The invoked skill |
| `inputs_used` | jsonb | YES | — | Input artifacts/steps consumed by this step. On an entry point's row, the entry record (below) |
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

UNIQUE constraint: (`project_slug`, `step_number`, `run`), so the feature path can run Steps 12 to 16 again for every feature.

**The entry record** is the `inputs_used` of the run's entry-point row (`step_number` `02` to `10`). It is written once, when the entry is taken, and every step of the run reads it from there. Its fields and values are set in [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md). The only foreign key on `steps` is
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

A `gates` row is written only by the developer, with `bash /mnt/c/mybizz/scripts/pdlf-gate.sh {slug} {gate} {run}`. Cupcake's rule `no_agent_gate_approval` blocks any agent from running that script or writing to this table; agents only read it.
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

| Column | Type | Notes |
|---|---|---|
| `id` | serial | Primary key |
| `step_id` | integer | FK → `steps(id)`. Identifies which feature-cycle execution this finding belongs to. |
| `finding_id` | text | Stable identifier from Steps 37–38 findings; a free-standing identifier with no companion table. |
| `source_step` | text | Which step produced this finding: `11, 12, 14, 15, 16, 17, 19, 20, 21, 34, 35, 35A, 36, 37, 38, 38A, 39, 40, 41, 42A, 43, 44, 45, 46` (CHECK). Every step that records a finding: Sentinel's steps and the steps whose test specifications record test failures |
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

1. **The ledger is the single source of truth.** If it is not in `pdlf`, it did not happen.
2. **Step sequencing is enforced by the orchestrator, not the database.** The only foreign key on `steps` is `project_slug → projects(slug)`; there is no inter-step constraint. Step dependencies vary per step and are held in the orchestrator's run order ([[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md)). The orchestrator checks that order before writing a step's ledger row; that is the enforcement point. A database trigger would need a second, hand-maintained copy of the dependency graph, with nothing keeping the two in step. The only legitimate writer is OpenCode, operating through a PDLF step; a raw write that bypasses the orchestrator is a policy violation before it reaches the schema.
3. **Step Receipts are generated from ledger rows.** The receipt IS the ledger row, formatted for reading — not a separately composed summary.
4. **No other register.** There is no state file, log or completion report beside the ledger.
5. **No narrative gloss can diverge from what actually happened.** The receipt is a snapshot of the row at the time it was written.
