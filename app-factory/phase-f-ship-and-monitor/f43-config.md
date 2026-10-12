---
title: "f43-config"
doc-id: "mb-c55a9572"
updated: "2026-10-12"
---

## From `step-mapping.md`: this step's rows

### Phase E — Ship & Monitor

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 43 | `[[step-43-staging-smoke-test]]` | Skill | GStack [[[makepdlf-project-library:stepwise/step-38-qa\|/qa]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-38-qa.md) or `/canary` — smoke test | |

### Phase E — Ship & Monitor: phase notes

**Note:** Steps 42, 42A, 43, and 44 are flagged for rebuild — see `ToDo.md` item 2. They
currently model a staging/production environment split that does not apply to this
platform (see `[[adr-no-staging-environment-five-app-isolation]]`). Listed here as
currently defined; not yet corrected.


Exit gates: `production-released` (Step 44), `released` (Step 46). For entry condition
and dependencies, see [[[makepdlf-project-library:stepwise/run-plan|Run Plan]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/run-plan.md).

## From `bft-checkpoint-cheatsheet-v2.md`: BFT level

### Phase F — Ship & Monitor (Steps 41–46)

| Step | Name | Type | BFT | Rationale |
|---|---|---|---|---|
| 43 | /qa or /canary at Staging | Skill | **Full** | Smoke test against live Staging — verification decisions before production promotion |
