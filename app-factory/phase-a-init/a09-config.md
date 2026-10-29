---
title: "a09-config"
doc-id: "mb-77e5e2b5"
updated: "2026-10-29"
---
# Step 9 — Feature for App 3 or App 5: Configuration

The fixed values of Step 9. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-a-init/a09-reference|Step 9 Reference]]](C:/pdlf/app-factory/phase-a-init/a09-reference.md). What the step is and why: [[[pdlf:app-factory/phase-a-init/a09-explainer|Step 9 Explainer]]](C:/pdlf/app-factory/phase-a-init/a09-explainer.md). What it must prove: [[[pdlf:app-factory/phase-a-init/a09-test-spec|Step 9 Test Specification]]](C:/pdlf/app-factory/phase-a-init/a09-test-spec.md). The values every entry point shares (the entry record's fields, the ledger values, the routes) are in [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md).

## Identity

| Item | Value |
|---|---|
| Step | 9, entry point `add-feature-management-app` |
| Phase | A, Init |
| Carried out by | The orchestrator (Step 1) |
| App worked on | App 3 or 5 |
| Run | the feature slug |
| Route | Feature |
| Joins the pipeline at | Step 12, route C |
| Health check first | Yes: [[[pdlf:pdlf-library/operating-procedures/sop-health-check\|SOP: Health Check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md) |
| Gate | None |
| BFT level | Light |
| Sentinel scrutiny | None |

## Questions to David

| Question | Recorded as |
|---|---|
| Which app: 3 or 5 | `app_number` |
| The feature, in David's words | `statement` |
| The feature's short name | `run` |

## The entry record

`route` `feature`, `app_number` 3 or 5, `run` the feature slug, `statement`, `start_step` `12`.

## The baseline suite

| Item | Value |
|---|---|
| App | App 5, when App 5 is the app worked on |
| Commands | `bash /mnt/c/dev/project-library-global/test-suite/tools/ts_local.sh /mnt/c/dev/dev-{slug}/{slug}-app5 start`; `bash /mnt/c/dev/project-library-global/test-suite/tools/ts_local.sh /mnt/c/dev/dev-{slug}/{slug}-app5 run pytest tests --junitxml=/mnt/c/dev/dev-{slug}/{slug}-project-library/pdlf-outputs/a09/{slug}-a09-{run}-suite.xml`; `bash /mnt/c/dev/project-library-global/test-suite/tools/ts_local.sh /mnt/c/dev/dev-{slug}/{slug}-app5 stop` |
| A failure | Recorded in the checks file as a finding of the existing app; the entry continues |

## Outputs

| Output | Where |
|---|---|
| Health check report | `{slug}-project-library\pdlf-outputs\a09\{slug}-a09-{run}-health-check.md` |
| Baseline suite results (App 5) | `{slug}-project-library\pdlf-outputs\a09\{slug}-a09-{run}-suite.xml` |
| Test results | `{slug}-project-library\pdlf-outputs\a09\{slug}-a09-{run}-checks.xml` (JUnit XML, `ts-method` section 5) |
| Step Receipt | `{slug}-project-library\pdlf-outputs\a09\{slug}-a09-{run}-receipt.md` |
