---
title: "a02-config"
doc-id: "mb-052a9eac"
updated: "2026-10-29"
---
# Step 2 — New application, no context: Configuration

The fixed values of Step 2. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-a-init/a02-reference|Step 2 Reference]]](C:/pdlf/app-factory/phase-a-init/a02-reference.md). What the step is and why: [[[pdlf:app-factory/phase-a-init/a02-explainer|Step 2 Explainer]]](C:/pdlf/app-factory/phase-a-init/a02-explainer.md). What it must prove: [[[pdlf:app-factory/phase-a-init/a02-test-spec|Step 2 Test Specification]]](C:/pdlf/app-factory/phase-a-init/a02-test-spec.md). The values every entry point shares (the entry record's fields, the ledger values, the routes) are in [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md).

## Identity

| Item | Value |
|---|---|
| Step | 2, entry point `new-app-no-context` |
| Phase | A, Init |
| Carried out by | The orchestrator (Step 1) |
| App worked on | App 1 |
| Run | `app1` |
| Route | Application |
| Joins the pipeline at | Step 11, route A |
| Health check first | No |
| Gate | None |
| BFT level | Light |
| Sentinel scrutiny | None |

## Questions to David

| Question | Recorded as |
|---|---|
| The business's name | `projects.project_name` |
| The mode: `full` or `test` | `projects.mode` |

## The entry record

`route` `application`, `app_number` 1, `run` `app1`, `start_step` `11`; every other field `null` or `false`.

## Outputs

| Output | Where |
|---|---|
| Test results | `{slug}-project-library\pdlf-outputs\a02\{slug}-a02-{run}-checks.xml` (JUnit XML, `ts-method` section 5) |
| Step Receipt | `{slug}-project-library\pdlf-outputs\a02\{slug}-a02-{run}-receipt.md`, written by Step 11 once the project library exists |
