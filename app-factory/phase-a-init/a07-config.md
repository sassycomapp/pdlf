---
title: "a07-config"
doc-id: "mb-0b4e0294"
updated: "2026-10-29"
---
# Step 7 — Create App 3: Configuration

The fixed values of Step 7. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-a-init/a07-reference|Step 7 Reference]]](C:/pdlf/app-factory/phase-a-init/a07-reference.md). What the step is and why: [[[pdlf:app-factory/phase-a-init/a07-explainer|Step 7 Explainer]]](C:/pdlf/app-factory/phase-a-init/a07-explainer.md). What it must prove: [[[pdlf:app-factory/phase-a-init/a07-test-spec|Step 7 Test Specification]]](C:/pdlf/app-factory/phase-a-init/a07-test-spec.md). The values every entry point shares (the entry record's fields, the ledger values, the routes) are in [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md).

## Identity

| Item | Value |
|---|---|
| Step | 7, entry point `create-client-template` |
| Phase | A, Init |
| Carried out by | The orchestrator (Step 1) |
| App worked on | App 3 |
| Run | `app3` |
| Route | Client template |
| Joins the pipeline at | Step 11, route C |
| Health check first | Yes: [[[pdlf:pdlf-library/operating-procedures/sop-health-check\|SOP: Health Check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md) |
| Gate | None |
| BFT level | Light |
| Sentinel scrutiny | None |

## Questions to David

| Question | Recorded as |
|---|---|
| Whether App 3 already exists | `existing_apps` |

## The entry record

`route` `client-template`, `app_number` 3, `run` `app3`, `start_step` `11`, `existing_apps`.

## Outputs

| Output | Where |
|---|---|
| Health check report | `{slug}-project-library\pdlf-outputs\a07\{slug}-a07-{run}-health-check.md` |
| Test results | `{slug}-project-library\pdlf-outputs\a07\{slug}-a07-{run}-checks.xml` (JUnit XML, `ts-method` section 5) |
| Step Receipt | `{slug}-project-library\pdlf-outputs\a07\{slug}-a07-{run}-receipt.md` |
