---
title: "a05-config"
doc-id: "mb-ead752a8"
updated: "2026-10-29"
---
# Step 5 — Update to App 1: Configuration

The fixed values of Step 5. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-a-init/a05-reference|Step 5 Reference]]](C:/pdlf/app-factory/phase-a-init/a05-reference.md). What the step is and why: [[[pdlf:app-factory/phase-a-init/a05-explainer|Step 5 Explainer]]](C:/pdlf/app-factory/phase-a-init/a05-explainer.md). What it must prove: [[[pdlf:app-factory/phase-a-init/a05-test-spec|Step 5 Test Specification]]](C:/pdlf/app-factory/phase-a-init/a05-test-spec.md). The values every entry point shares (the entry record's fields, the ledger values, the routes) are in [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md).

## Identity

| Item | Value |
|---|---|
| Step | 5, entry point `update-main-app` |
| Phase | A, Init |
| Carried out by | The orchestrator (Step 1) |
| App worked on | App 1 |
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
| The update, in David's words | `statement` |
| The update's short name | `run` |
| Whether it changes what the app does | `route` |
| Whether it corrects a fault | `fault` |
| For an Update run: the step to start from | `start_step` |

## The entry record

`route` `feature` or `update`, `app_number` 1, `run` the update slug, `statement`, `fault`, `start_step` `12` for a Feature run or the step David names.

## The baseline suite

| Item | Value |
|---|---|
| App | App 1 |
| Commands | `bash /mnt/c/dev/project-library-global/test-suite/tools/ts_local.sh /mnt/c/dev/dev-{slug}/{slug}-app1 start`; `bash /mnt/c/dev/project-library-global/test-suite/tools/ts_local.sh /mnt/c/dev/dev-{slug}/{slug}-app1 run pytest tests --junitxml=/mnt/c/dev/dev-{slug}/{slug}-project-library/pdlf-outputs/a05/{slug}-a05-{run}-suite.xml`; `bash /mnt/c/dev/project-library-global/test-suite/tools/ts_local.sh /mnt/c/dev/dev-{slug}/{slug}-app1 stop` |
| A failure | Recorded in the checks file as a finding of the existing app; the entry continues |

## Outputs

| Output | Where |
|---|---|
| Health check report | `{slug}-project-library\pdlf-outputs\a05\{slug}-a05-{run}-health-check.md` |
| Baseline suite results (App 1) | `{slug}-project-library\pdlf-outputs\a05\{slug}-a05-{run}-suite.xml` |
| Diagnosis, when the update corrects a fault | `{slug}-project-library\pdlf-outputs\a05\{slug}-a05-{run}-diagnosis.md` |
| Test results | `{slug}-project-library\pdlf-outputs\a05\{slug}-a05-{run}-checks.xml` (JUnit XML, `ts-method` section 5) |
| Step Receipt | `{slug}-project-library\pdlf-outputs\a05\{slug}-a05-{run}-receipt.md` |
