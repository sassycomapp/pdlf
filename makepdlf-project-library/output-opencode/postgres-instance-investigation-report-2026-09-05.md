---
title: "postgres-instance-investigation-report-2026-09-05"
doc-id: "mb-3d2ddba2"
updated: "2026-10-09"
---
# PostgreSQL Instance Investigation Report — 2026-09-05

**Task:** Complete, systematic investigation of every PostgreSQL instance on this machine,
cross-checked against GBrain memory. All checks were read-only.

**Agent:** OpenCode Build (makepdlf-project-library)
**Timestamp:** 2026-09-05T160554+0200
**Verification basis:** every fact below was verified live this session unless marked
`[INF]` (inference, not upgraded to fact) or `[DOC]` (from an authoritative file).

---

## 1. Executive summary

- Exactly **two live PostgreSQL clusters** exist: Windows PostgreSQL 15.14 (the PDLF
  ledger host) and WSL PostgreSQL 16.14 (the GBrain host). **No third instance.**
- The Windows `pdlf` database matches the seven-table spec **at table level**, but the
  spec's column-level definitions are stale for **six of seven tables**. Only
  `triage_findings` matches exactly.
- **Every table in `pdlf` is empty (0 rows).** The ledger currently records nothing.
- **No database named `compliance_ledger` exists on Windows** (verified by full
  enumeration) and **no GBrain source mentions one** (verified across all 12 sources).
  The WSL cluster could not be enumerated this session (harness policy blocks) — it is
  the only remaining possible location; a developer-run script is provided in §6.
- GBrain's own memory documents itself as "Local PGLite" in two project docs — **stale**;
  the live engine is PostgreSQL (database `gbrain` on the WSL 16 cluster).

---

## 2. Instance A — Windows PostgreSQL 15.14 (PDLF ledger host)

| Item | Finding | Certainty |
|---|---|---|
| Installation | `C:\Program Files\PostgreSQL\15\`; Windows registry shows exactly one PostgreSQL product (15.14-1) | [LIVE] |
| Services | `postgresql-x64-15` Running (Automatic); a second service named `PostgreSQL` is Stopped (Automatic) — **both registrations point to the same data directory** `C:\Program Files\PostgreSQL\15\data`. One cluster with a duplicate service registration, not two instances. Undocumented. | [LIVE] |
| Reachability | `pg_isready` (Windows side): accepting connections on 127.0.0.1:5432 | [LIVE] |
| Auth | `pg_hba.conf`: `scram-sha-256` for all users/addresses incl. `0.0.0.0/0` and `::/0`; no trust paths. `listen_addresses`/`port` left at defaults (localhost:5432) | [LIVE] |
| Roles | `postgres`, `pdlf_agent`, `pgvector_user` (leftover from the pgvector era; undocumented) | [LIVE] |
| Extensions | `pdlf` DB: `plpgsql` only. `postgres` DB: `adminpack`, `btree_gist`, `pg_stat_statements`, `pg_trgm`, `plpgsql`, `vector 0.8.0` | [LIVE] |

### Databases (excluding template0/template1)

| Database | Owner | Size | Status |
|---|---|---|---|
| `pdlf` | pdlf_agent | 7,877 kB | Live infrastructure; **all seven tables empty (0 rows)** |
| `postgres` | postgres | 14 MB | Graveyard of AI-memory experiments (see below) — stale/test, effectively abandoned |

### `pdlf` — table inventory (complete, [LIVE])

Exactly the seven spec tables in schema `public`, all owned by `pdlf_agent`, nothing else:
`bft_records`, `deviations`, `gates`, `isc`, `projects`, `steps`, `triage_findings`.

**Row counts [LIVE]:** projects 0, steps 0, gates 0, deviations 0, bft_records 0, isc 0,
triage_findings 0.

**Schema drift vs `[[spec-postgres-ledger]]` [LIVE vs DOC]:**

| Table | Spec says | Live reality | Drift |
|---|---|---|---|
| `projects` | slug, name, mode, paths (jsonb), gbrain_sources (text[]), is_active | slug, **project_name**, mode, **library_path**, **code_path**, **anvil_slug**, **gbrain_source_docs**, **gbrain_source_code**, is_active, **created_at** | Stale |
| `steps` | step_number (integer), type, status, synthesized, artifact_path, next_action | **19 columns**: id, project_slug, **step_number (text)**, sort_order, phase, **step_type**, skill_family, skill_name, inputs_used (jsonb), artifact_path, synthesized (bool), status, next_action, started_at, completed_at, blockers, notes_for_next_session, gbrain_query, gbrain_results | Stale |
| `gates` | gate_name, passed, approved_at | id, project_slug, step_id, gate_name, passed, approved_at, **notes** | Stale |
| `deviations` | description, options_presented, decision | id, project_slug, step_id, description, options_presented, decision, **decided_at** | Stale |
| `bft_records` | level, bones..health (7 cols) | **12 columns**: id, project_slug, step_id, gate_id, level, bones, muscle, nerves, fat, skin, health, recorded_at | Stale |
| `isc` | isc_number (integer), description, verify_method, status (pending/passed/failed), evidence | id, project_slug, **isc_number (text)**, description, verify_method, status (**pending/verified/failed**), evidence, **updated_at** | Stale |
| `triage_findings` | 17 columns incl. security-review set | **17/17 columns match exactly** (incl. concern/asset/threat/evidence/severity/confidence/recommended_control/verification) | Match |

**Constraints [LIVE]:** FKs confirmed: `triage_findings.step_id → steps(id)`; the only FK on
`steps` is `project_slug → projects(slug)` (matches spec Principle 2). Additional FKs the
spec does not mention: bft_records → gates(id), steps(id), projects(slug); deviations and
gates → steps(id) and projects(slug); isc → projects(slug). CHECK constraints live values
differ from spec: `isc_status_check` allows `verified` (spec says `passed`);
`triage_findings_triage_label_check` includes `clear` (spec lists five labels without it);
`steps_status_check` includes `blocked` and does **not** include `synthesized` (spec wrong —
`synthesized` is a boolean column); `steps_step_type_check` uses lowercase
`skill/manual/optional/gate` (spec says uppercase); `steps_skill_family_check` allows
gstack/matt-skills/opencode/manual/NULL. `steps` UNIQUE (project_slug, step_number);
`isc` UNIQUE (project_slug, isc_number).

### `postgres` maintenance DB — user tables (complete, [LIVE])

`public`: departments (1), diary_cache (0), episodic_memory (0),
episodic_memory_2023 (0), episodic_memory_partitioned (0), episodic_memory_y2025m10 (0),
global_cache (0), other_table (0), products (2), roles (2), semantic_cache (0),
semantic_cache_entries (0), semantic_memory (2), test_performance (100),
test_python_integration (10), test_similarity (4), test_table (0), test_vector_10 (3),
test_vector_128 (3), test_vector_3 (3), test_vector_5 (3), test_vector_512 (3),
test_vector_table (3), test_vectors (2), users (3), vector_cache (0),
vector_search_test (100), working_memory (2).
`vecs`: mem0_memories (0), mem0migrations (1).

Character: mem0 framework + pgvector + episodic/semantic/working-memory + RAG-cache
experimentation, plus a family of `test_vector_*` tables. [INF] Remains of an agent-memory
experimentation phase, superseded by the current GBrain-on-PostgreSQL setup. Undocumented.

---

## 3. Instance B — WSL-native PostgreSQL 16.14 (GBrain host)

| Item | Finding | Certainty |
|---|---|---|
| Cluster | `pg_lsclusters`: `16 main 5432 online postgres /var/lib/postgresql/16/main`; psql client 16.14 (Ubuntu 24.04 package) | [LIVE] |
| Listener | `127.0.0.1:5432` on the WSL side — **shares the port number with Windows but is a different, independent server** | [LIVE] |
| Purpose | Hosts GBrain's brain database `gbrain`, role `postgres` (GBrain's own config, password masked): engine `postgres`, 1,531 pages, 5,042 chunks, RLS on 62/62 public tables, schema version 128, embedding `openai:text-embedding-3-large` (1536d) | [LIVE] |
| Documentation | This cluster is documented nowhere in this project's files | [LIVE] (absence of hits) |
| Enumeration | Databases/extensions/tables/row counts **not obtainable this session**: harness policy blocked `sudo`, WSL-credential reuse, `/etc/postgresql/*`, `/var/lib/postgresql`, and `/etc/wsl.conf` reads | [LIVE] (the blocks) |

The config value `database_path: /home/dev-p/.gbrain/brain.pglite` still present in GBrain's
config is a stale leftover from the pre-migration PGLite era.

---

## 4. Third-instance search — CLOSED

- Windows registry uninstall entries: only "PostgreSQL 15" (15.14-1). No pgAdmin product
  listed machine-wide.
- Windows services: only the two registrations, both → `C:\Program Files\PostgreSQL\15\data`.
- No `C:\Program Files (x86)\PostgreSQL\`, no `C:\PostgreSQL\`.
- WSL Ubuntu-24.04 (current distro): one cluster (`16/main`).
- WSL **Ubuntu-22.04** (second distro, stopped): **no PostgreSQL at all** — no `psql`
  binary, no clusters.
- No other listeners in the 543x port range on either side.
- [INF] A manually compiled, never-registered postgres cannot be 100% excluded, but no
  evidence of one exists.

---

## 5. compliance_ledger — verdict

- **GBrain memory, all 12 sources: zero mentions.** Probes run: `search "compliance_ledger"`,
  `search "compliance ledger database"`, broad all-source `query`, `recall` (facts arm),
  and a `think` multi-hop synthesis — all confirm the only documented database is `pdlf`.
- **Windows: definitively absent** — full database and table enumeration of both
  non-template databases shows no such database and no such table.
- **WSL: unverifiable this session** (enumeration blocked). [INF] It is the only place a
  `compliance_ledger` database could exist, most plausibly as an abandoned test/experiment
  database alongside `gbrain`. Run the §6 script to close this definitively.

---

## 6. Remaining blocked checks — developer-run script (read-only)

The harness blocks (not liftable from the agent side): `sudo`, `/etc/wsl.conf`,
`/etc/postgresql/*`, `/var/lib/postgresql`, and WSL-credential retrieval. Paste into a WSL
terminal:

```bash
# --- WSL Postgres full census (read-only) ---
cat /etc/wsl.conf
dpkg -l | grep -i postgres
sudo -u postgres psql -X -P pager=off \
  -c "SHOW config_file;" -c "SHOW hba_file;" \
  -c "SELECT name, setting FROM pg_settings WHERE name IN ('port','listen_addresses');" \
  -c "SELECT datname, pg_get_userbyid(datdba) AS owner, pg_size_pretty(pg_database_size(datname)) AS size, datallowconn FROM pg_database WHERE datistemplate = false ORDER BY 1;"
for db in $(sudo -u postgres psql -X -Atc "SELECT datname FROM pg_database WHERE datistemplate = false AND datallowconn ORDER BY 1"); do
  echo "===== DATABASE: $db ====="
  sudo -u postgres psql -X -d "$db" -P pager=off \
    -c "SELECT extname, extversion FROM pg_extension ORDER BY 1;" \
    -c "SELECT schemaname, tablename, tableowner FROM pg_tables WHERE schemaname NOT IN ('pg_catalog','information_schema') ORDER BY 1,2;"
  sudo -u postgres psql -X -d "$db" -P pager=off -Atc "
    SELECT schemaname||'.'||tablename||' = '||coalesce((xpath('/row/c/text()',
      query_to_xml(format('SELECT count(*) AS c FROM %I.%I', schemaname, tablename),
      false, true, '')))[1]::text,'ERROR')
    FROM pg_tables WHERE schemaname NOT IN ('pg_catalog','information_schema') ORDER BY 1,2;"
done
```

If a `compliance_ledger` database appears, additionally run:
`sudo -u postgres psql -d compliance_ledger -c "\dt+"`

---

## 7. Documentation contradictions (complete list)

1. **`[[config]]`** — "Brain type: Local PGLite" → **stale**; live engine is
   PostgreSQL (database `gbrain` on WSL 16.14).
2. **`[[system-description]]`** — "GBrain / PGlite" → **stale**, same reason.
3. **`[[spec-postgres-ledger]]`** schema section → **stale for 6 of 7
   tables** (detail in §2); needs a column-level rewrite from the live schema.
4. **Same spec**, "Do NOT attempt direct psql from WSL" → the rule is correct but the
   stated reason (binfmt env vars) is incomplete: WSL `localhost:5432` is now a
   *different cluster* (GBrain's). A direct WSL psql silently targets the wrong server.
5. **Spec Principle 1** ("If it's not in `pdlf`, it didn't happen") vs. reality: all seven
   tables are empty — the ledger currently records nothing.
6. **Undocumented:** the `postgres` DB experiment graveyard (mem0/pgvector era), the
   duplicate `PostgreSQL` service registration, the `pgvector_user` role, and the entire
   WSL PostgreSQL 16 cluster.
7. **`postgresql-reference.md` (mybizz-config-docs)** — referenced as existing documentation but **not found**:
   not in this repo, not in `C:\dev\project-library-global\`, no GBrain hit under that
   name. [INF] The name may refer to `[[config]]` or the spec itself.
8. Minor operational hazard: `.env` line 16 holds an unquoted Windows path (with spaces)
   that breaks shell `source`-ing. Values were not read.

---

## 8. GBrain health side-observations (out of scope, flagged only)

From `gbrain doctor` (read-only): 5 sources have stale sync (oldest ~20 days); 3
embed-backfill jobs queued ~844h with no live worker; brain score 57/100. Optional
cleanup, separate from this investigation.

---

## 9. Next steps

- **Developer:** run the §6 script; paste output to close the `compliance_ledger` question.
- **Build (requires explicit approval):** update `[[spec-postgres-ledger]]` (column-level
  rewrite + corrected WSL warning), `[[config]]` and
  `[[system-description]]` (PGLite → postgres); decide on cleanup for the
  duplicate service, `pgvector_user` role, and the `postgres`-DB graveyard.
- **Housekeeping:** report artefact saved to `output-opencode/`; devlog-index and
  judgement-trail entries recorded per project AGENTS.md audit-trail rule.

---

*Report generated by OpenCode Build agent, 2026-09-05T160554+0200. Investigation performed
entirely with read-only commands against the live systems.*
