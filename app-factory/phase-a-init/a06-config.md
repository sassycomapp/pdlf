---
title: "a06-config"
doc-id: "mb-93fc7e2a"
updated: "2026-10-29"
---
# Step 6 — Release into App 2: Configuration

The fixed values of Step 6. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-a-init/a06-reference|Step 6 Reference]]](C:/pdlf/app-factory/phase-a-init/a06-reference.md). What the step is and why: [[[pdlf:app-factory/phase-a-init/a06-explainer|Step 6 Explainer]]](C:/pdlf/app-factory/phase-a-init/a06-explainer.md). What it must prove: [[[pdlf:app-factory/phase-a-init/a06-test-spec|Step 6 Test Specification]]](C:/pdlf/app-factory/phase-a-init/a06-test-spec.md). The values every entry point shares (the entry record's fields, the ledger values, the routes) are in [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md).

## Identity

| Item | Value |
|---|---|
| Step | 6, entry point `compile-master-template` |
| Phase | A, Init |
| Carried out by | The orchestrator (Step 1) |
| App worked on | App 2 |
| Run | `app2` |
| Route | Release |
| Joins the pipeline at | Step 41 |
| Health check first | Yes: [[[pdlf:pdlf-library/operating-procedures/sop-health-check\|SOP: Health Check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md) |
| Gate | None |
| BFT level | Light |
| Sentinel scrutiny | None |

## Questions to David

| Question | Recorded as |
|---|---|
| Confirmation that App 1's approved work is to be released into App 2 | `route` |

## The entry record

`route` `release`, `app_number` 2, `run` `app2`, `start_step` `41`.

## The baseline suite

| Item | Value |
|---|---|
| App | App 1 |
| Commands | `bash /mnt/c/dev/project-library-global/test-suite/tools/ts_local.sh /mnt/c/dev/dev-{slug}/{slug}-app1 start`; `bash /mnt/c/dev/project-library-global/test-suite/tools/ts_local.sh /mnt/c/dev/dev-{slug}/{slug}-app1 run pytest tests --junitxml=/mnt/c/dev/dev-{slug}/{slug}-project-library/pdlf-outputs/a06/{slug}-a06-{run}-suite.xml`; `bash /mnt/c/dev/project-library-global/test-suite/tools/ts_local.sh /mnt/c/dev/dev-{slug}/{slug}-app1 stop` |
| A failure | Stops the entry: a release starts only from a passing App 1 |

## Outputs

| Output | Where |
|---|---|
| Health check report | `{slug}-project-library\pdlf-outputs\a06\{slug}-a06-{run}-health-check.md` |
| Baseline suite results (App 1) | `{slug}-project-library\pdlf-outputs\a06\{slug}-a06-{run}-suite.xml` |
| Test results | `{slug}-project-library\pdlf-outputs\a06\{slug}-a06-{run}-checks.xml` (JUnit XML, `ts-method` section 5) |
| Step Receipt | `{slug}-project-library\pdlf-outputs\a06\{slug}-a06-{run}-receipt.md` |
