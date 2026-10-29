---
title: "a10-config"
doc-id: "mb-46b8aeb3"
updated: "2026-10-29"
---
# Step 10 — Update to App 3 or App 5: Configuration

The fixed values of Step 10. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-a-init/a10-reference|Step 10 Reference]]](C:/pdlf/app-factory/phase-a-init/a10-reference.md). What the step is and why: [[[pdlf:app-factory/phase-a-init/a10-explainer|Step 10 Explainer]]](C:/pdlf/app-factory/phase-a-init/a10-explainer.md). What it must prove: [[[pdlf:app-factory/phase-a-init/a10-test-spec|Step 10 Test Specification]]](C:/pdlf/app-factory/phase-a-init/a10-test-spec.md). The values every entry point shares (the entry record's fields, the ledger values, the routes) are in [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md).

## Identity

| Item | Value |
|---|---|
| Step | 10, entry point `update-management-app` |
| Phase | A, Init |
| Carried out by | The orchestrator (Step 1) |
| App worked on | App 3 or 5 |
| Run | the update slug |
| Route | Feature, when the update changes what the app does; otherwise Update |
| Joins the pipeline at | Step 12 for a Feature run; otherwise the step David names |
| Health check first | Yes: [[[pdlf:pdlf-library/operating-procedures/sop-health-check\|SOP: Health Check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md) |
| Gate | None |
| BFT level | Light |
| Sentinel scrutiny | None |

## Questions to David

| Question | Recorded as |
|---|---|
| Which app: 3 or 5 | `app_number` |
| The update, in David's words | `statement` |
| The update's short name | `run` |
| Whether it changes what the app does | `route` |
| Whether it corrects a fault | `fault` |
| For an Update run: the step to start from | `start_step` |

## The entry record

`route` `feature` or `update`, `app_number` 3 or 5, `run` the update slug, `statement`, `fault`, `start_step` `12` for a Feature run or the step David names.

## The baseline suite

| Item | Value |
|---|---|
| App | App 5, when App 5 is the app worked on |
| Commands | `bash /mnt/c/dev/project-library-global/test-suite/tools/ts_local.sh /mnt/c/dev/dev-{slug}/{slug}-app5 start`; `bash /mnt/c/dev/project-library-global/test-suite/tools/ts_local.sh /mnt/c/dev/dev-{slug}/{slug}-app5 run pytest tests --junitxml=/mnt/c/dev/dev-{slug}/{slug}-project-library/pdlf-outputs/a10/{slug}-a10-{run}-suite.xml`; `bash /mnt/c/dev/project-library-global/test-suite/tools/ts_local.sh /mnt/c/dev/dev-{slug}/{slug}-app5 stop` |
| A failure | Recorded in the checks file as a finding of the existing app; the entry continues |

## Outputs

| Output | Where |
|---|---|
| Health check report | `{slug}-project-library\pdlf-outputs\a10\{slug}-a10-{run}-health-check.md` |
| Baseline suite results (App 5) | `{slug}-project-library\pdlf-outputs\a10\{slug}-a10-{run}-suite.xml` |
| Diagnosis, when the update corrects a fault | `{slug}-project-library\pdlf-outputs\a10\{slug}-a10-{run}-diagnosis.md` |
| Test results | `{slug}-project-library\pdlf-outputs\a10\{slug}-a10-{run}-checks.xml` (JUnit XML, `ts-method` section 5) |
| Step Receipt | `{slug}-project-library\pdlf-outputs\a10\{slug}-a10-{run}-receipt.md` |
