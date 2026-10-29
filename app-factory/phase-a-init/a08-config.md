---
title: "a08-config"
doc-id: "mb-40ed67de"
updated: "2026-10-29"
---
# Step 8 — Create App 5: Configuration

The fixed values of Step 8. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-a-init/a08-reference|Step 8 Reference]]](C:/pdlf/app-factory/phase-a-init/a08-reference.md). What the step is and why: [[[pdlf:app-factory/phase-a-init/a08-explainer|Step 8 Explainer]]](C:/pdlf/app-factory/phase-a-init/a08-explainer.md). What it must prove: [[[pdlf:app-factory/phase-a-init/a08-test-spec|Step 8 Test Specification]]](C:/pdlf/app-factory/phase-a-init/a08-test-spec.md). The values every entry point shares (the entry record's fields, the ledger values, the routes) are in [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md).

## Identity

| Item | Value |
|---|---|
| Step | 8, entry point `create-management-app` |
| Phase | A, Init |
| Carried out by | The orchestrator (Step 1) |
| App worked on | App 5 |
| Run | `app5` |
| Route | Management app |
| Joins the pipeline at | Step 11, route C |
| Health check first | Yes: [[[pdlf:pdlf-library/operating-procedures/sop-health-check\|SOP: Health Check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md) |
| Gate | None |
| BFT level | Light |
| Sentinel scrutiny | None |

## Questions to David

| Question | Recorded as |
|---|---|
| Whether App 5 already exists | `existing_apps` |

## The entry record

`route` `management-app`, `app_number` 5, `run` `app5`, `start_step` `11`, `existing_apps`.

## Outputs

| Output | Where |
|---|---|
| Health check report | `{slug}-project-library\pdlf-outputs\a08\{slug}-a08-{run}-health-check.md` |
| Test results | `{slug}-project-library\pdlf-outputs\a08\{slug}-a08-{run}-checks.xml` (JUnit XML, `ts-method` section 5) |
| Step Receipt | `{slug}-project-library\pdlf-outputs\a08\{slug}-a08-{run}-receipt.md` |
