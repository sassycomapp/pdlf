---
title: "f42a-config"
doc-id: "mb-1de372f7"
updated: "2026-11-13"
---
# Step 42A — Release Regression: Configuration

The fixed values of Step 42A. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-f-ship-and-monitor/f42a-reference|Step 42A Reference]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f42a-reference.md). What the step is and why: [[[pdlf:app-factory/phase-f-ship-and-monitor/f42a-explainer|Step 42A Explainer]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f42a-explainer.md). What it must prove: [[[pdlf:app-factory/phase-f-ship-and-monitor/f42a-test-spec|Step 42A Test Specification]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f42a-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 42A, Release Regression |
| Phase | F, Ship and Monitor |
| Carried out by | OpenCode, with the skills below |
| Runs for | App 1 and App 5 runs, and every release |
| Previous step | 42 |
| Next step | 43 |
| Gate | None |
| BFT level | Light |
| Sentinel scrutiny | None |
| Conditional | Skipped for an App 5 run |

## Inputs

| Input | Where |
|---|---|
| Test client instance | Its address, with a `TEST_` user for each role |
| Test plan | `{slug}-project-library\docs-local\design\{run}\test-plan.md` |
| Assessment plan | `{slug}-project-library\docs-local\design\app{n}\threat-model.md` |

## Outputs

| Output | Where |
|---|---|
| Findings | `pdlf-outputs\f42a\{slug}-f42a-{run}-findings.md` |
| Dynamic scan | `pdlf-outputs\f42a\{slug}-f42a-{run}-scan.md` |
| Ledger | the Step 42A `steps` row; its BFT record |
| Test results | `pdlf-outputs\f42a\{slug}-f42a-{run}-checks.xml` |
| Step Receipt | `pdlf-outputs\f42a\{slug}-f42a-{run}-receipt.md` |

All paths without a repository name are inside `{slug}-project-library\`.

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `42A` |
| `step_type` | `skill` |
| `skill_family` | `gstack` |
| `run` | From the entry record |
| `ticket` | Empty |
| `app_number` | From the entry record |
| `status` | `complete` when every flow passes; `skipped` for App 5 |
| `synthesized` | `false` |
| `artifact_path` | `pdlf-outputs\f42a\{slug}-f42a-{run}-findings.md` |
| `inputs_used` | Step 42 |
