---
title: "a04-config"
doc-id: "mb-6c5ff3d0"
updated: "2026-10-29"
---
# Step 4 — Feature for App 1: Configuration

The fixed values of Step 4. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-a-init/a04-reference|Step 4 Reference]]](C:/pdlf/app-factory/phase-a-init/a04-reference.md). What the step is and why: [[[pdlf:app-factory/phase-a-init/a04-explainer|Step 4 Explainer]]](C:/pdlf/app-factory/phase-a-init/a04-explainer.md). What it must prove: [[[pdlf:app-factory/phase-a-init/a04-test-spec|Step 4 Test Specification]]](C:/pdlf/app-factory/phase-a-init/a04-test-spec.md). The values every entry point shares (the entry record's fields, the ledger values, the routes) are in [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md).

## Identity

| Item | Value |
|---|---|
| Step | 4, entry point `add-feature-main-app` |
| Phase | A, Init |
| Carried out by | The orchestrator (Step 1) |
| App worked on | App 1 |
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
| The feature, in David's words; a whole release specification kept in `docs-local\releases\v{n}\` may be named instead | `statement` |
| The feature's short name | `run` |

## The entry record

`route` `feature`, `app_number` 1, `run` the feature slug, `statement`, `start_step` `12`.

## The baseline suite

| Item | Value |
|---|---|
| App | App 1 |
| Commands | `bash /mnt/c/dev/project-library-global/test-suite/tools/ts_local.sh /mnt/c/dev/dev-{slug}/{slug}-app1 start`; `bash /mnt/c/dev/project-library-global/test-suite/tools/ts_local.sh /mnt/c/dev/dev-{slug}/{slug}-app1 run pytest tests --junitxml=/mnt/c/dev/dev-{slug}/{slug}-project-library/pdlf-outputs/a04/{slug}-a04-{run}-suite.xml`; `bash /mnt/c/dev/project-library-global/test-suite/tools/ts_local.sh /mnt/c/dev/dev-{slug}/{slug}-app1 stop` |
| A failure | Recorded in the checks file as a finding of the existing app; the entry continues |

## Outputs

| Output | Where |
|---|---|
| Health check report | `{slug}-project-library\pdlf-outputs\a04\{slug}-a04-{run}-health-check.md` |
| Baseline suite results (App 1) | `{slug}-project-library\pdlf-outputs\a04\{slug}-a04-{run}-suite.xml` |
| Test results | `{slug}-project-library\pdlf-outputs\a04\{slug}-a04-{run}-checks.xml` (JUnit XML, `ts-method` section 5) |
| Step Receipt | `{slug}-project-library\pdlf-outputs\a04\{slug}-a04-{run}-receipt.md` |
