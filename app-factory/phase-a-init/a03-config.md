---
title: "a03-config"
doc-id: "mb-235785c2"
updated: "2026-10-29"
---
# Step 3 — New application with context: Configuration

The fixed values of Step 3. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-a-init/a03-reference|Step 3 Reference]]](C:/pdlf/app-factory/phase-a-init/a03-reference.md). What the step is and why: [[[pdlf:app-factory/phase-a-init/a03-explainer|Step 3 Explainer]]](C:/pdlf/app-factory/phase-a-init/a03-explainer.md). What it must prove: [[[pdlf:app-factory/phase-a-init/a03-test-spec|Step 3 Test Specification]]](C:/pdlf/app-factory/phase-a-init/a03-test-spec.md). The values every entry point shares (the entry record's fields, the ledger values, the routes) are in [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md).

## Identity

| Item | Value |
|---|---|
| Step | 3, entry point `new-app-with-context` |
| Phase | A, Init |
| Carried out by | The orchestrator (Step 1) |
| App worked on | App 1 |
| Run | `app1` |
| Route | Application |
| Joins the pipeline at | Step 11, route B |
| Health check first | No |
| Gate | None |
| BFT level | Light |
| Sentinel scrutiny | None |

## Questions to David

| Question | Recorded as |
|---|---|
| The business's name | `projects.project_name` |
| The mode: `full` or `test` | `projects.mode` |
| Which apps already exist: 1, 2, 3, 5 | `existing_apps` |
| Whether the business's existing project library holds its context | `project_context` |
| Whether the application follows a reference platform, which, and where its material is kept | `reference_platform` |

## The entry record

`route` `application`, `app_number` 1, `run` `app1`, `start_step` `11`, `existing_apps`, `project_context` and `reference_platform` from David's answers.

## Outputs

| Output | Where |
|---|---|
| Test results | `{slug}-project-library\pdlf-outputs\a03\{slug}-a03-{run}-checks.xml` (JUnit XML, `ts-method` section 5) |
| Step Receipt | `{slug}-project-library\pdlf-outputs\a03\{slug}-a03-{run}-receipt.md`, written by Step 11 once the project library exists |
