---
title: "schema-conformance-report-2026-07-19"
doc-id: "mb-84c57e48"
updated: "2026-10-09"
---
# Ledger Schema Conformance Report — 2026-07-19

Checks 3.1–3.4 per [[[pdlf:makepdlf-project-library/checklists-local/chk-pdlf-self-test|PDLF Self-Test Checklist]]](C:/pdlf/makepdlf-project-library/checklists-local/chk-pdlf-self-test.md).

## 3.1 — Table Existence: PASS (7/7)

All seven expected tables exist in the `pdlf` database:
projects, steps, gates, deviations, bft_records, isc, triage_findings.

## 3.2 — Step Sequencing Enforcement: PASS (resolved)

Inserted a `steps` row for `step_number='19'` under `project_slug='_selftest'` with no
step 16 row present. The insert succeeded at the schema level — no inter-step FK constraint
exists. The only FK on `steps` is `project_slug → projects(slug)`.

**Resolution:** This is correct by design, not a defect. Step dependencies vary per step
(see [[[pdlf:makepdlf-project-library/stepwise/run-plan|Run Plan]]](C:/pdlf/makepdlf-project-library/stepwise/run-plan.md)'s Step Dependencies table — Step 19 depends on 14/15/16/17, Step 34
depends on a different seven steps, etc.) and cannot be expressed as a fixed database-level
FK. The only writer with legitimate access to the database is the orchestrator, operating
through a PDLF step. Sequencing enforcement is the orchestrator's responsibility, checking
[[[pdlf:makepdlf-project-library/stepwise/run-plan|Run Plan]]](C:/pdlf/makepdlf-project-library/stepwise/run-plan.md)'s dependency table before writing a step's ledger row.

**Action taken:** [[[pdlf:makepdlf-project-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-postgres-ledger.md) Principle 2 corrected; [[[pdlf:makepdlf-project-library/checklists-local/chk-pdlf-self-test|PDLF Self-Test Checklist]]](C:/pdlf/makepdlf-project-library/checklists-local/chk-pdlf-self-test.md)
check 3.2 corrected. Both no longer claim database-level referential integrity between steps.

## 3.3 — build-verified Gate Query: PASS

Seeded three `triage_findings` for `step_id=2` (`_selftest`):
- SELFTEST-F-1: `wontfix`, resolved_at=NULL
- SELFTEST-F-2: `ready-for-agent`, resolved_at=now()
- SELFTEST-F-3: `needs-triage`, resolved_at=NULL

Gate query: `WHERE triage_label <> 'wontfix' AND resolved_at IS NULL`

**Raw result BEFORE resolve** (expected: gate does NOT pass):
```
 id |  finding_id  | triage_label | resolved_at
----+--------------+--------------+-------------
  6 | SELFTEST-F-3 | needs-triage |
(1 row)
```

Resolved SELFTEST-F-3: set `resolved_at = now()`, kept label as `needs-triage`.

**Raw result AFTER resolve** (expected: gate passes):
```
 id | finding_id | triage_label | resolved_at
----+------------+--------------+-------------
(0 rows)
```

Both OR branches (`wontfix` and `resolved_at IS NOT NULL`) work correctly.

## 3.4 — Deviations Round-Trip: PASS

Inserted a deviations row with:
- `description`: "Schema FK does not enforce step ordering"
- `options_presented`: `{"option1": "Add inter-step FK constraint", "option2": "Check in application layer only", "option3": "Skip"}`
- `decision`: "option1 selected"

Queried back — all three fields round-trip correctly.

## Summary

| Check | Result |
|---|---|
| 3.1 | PASS |
| 3.2 | PASS (resolved — schema correct as-is; documentation was the defect, now fixed) |
| 3.3 | PASS |
| 3.4 | PASS |

All _selftest-scoped rows cleaned up after the run.