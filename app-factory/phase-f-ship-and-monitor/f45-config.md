---
title: "f45-config"
doc-id: "mb-165902b2"
updated: "2026-11-13"
---
# Step 45 — Production Check: Configuration

The fixed values of Step 45. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-f-ship-and-monitor/f45-reference|Step 45 Reference]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f45-reference.md). What the step is and why: [[[pdlf:app-factory/phase-f-ship-and-monitor/f45-explainer|Step 45 Explainer]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f45-explainer.md). What it must prove: [[[pdlf:app-factory/phase-f-ship-and-monitor/f45-test-spec|Step 45 Test Specification]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f45-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 45, Production Check |
| Phase | F, Ship and Monitor |
| Carried out by | OpenCode, with the skills below |
| Runs for | App 1 and App 5 runs, and every release |
| Previous step | 44 |
| Next step | 46 |
| Gate | None |
| BFT level | Full |
| Sentinel scrutiny | Medium |
| Conditional | No |

## Inputs

| Input | Where |
|---|---|
| Release record | `{slug}-project-library\pdlf-outputs\f44\` |
| Baselines | `pdlf-outputs\f43\{slug}-f43-{run}-baseline.md`; `pdlf-outputs\f41\{slug}-f41-{run}-benchmark.md` |
| Assessment plan | `{slug}-project-library\docs-local\design\app{n}\threat-model.md` |

## Thresholds

| Measure | Pass | Rollback trigger |
|---|---|---|
| Errors | Below 5% | Above 10% across instances |
| Response time | Within 20% of baseline | As the deployment specification sets out |
| Heartbeats | Every one arrives | As the deployment specification sets out |

## Outputs

| Output | Where |
|---|---|
| Production report | `pdlf-outputs\f45\{slug}-f45-{run}-production.md` |
| Ledger | the Step 45 `steps` row; its BFT record; its `triage_findings` row |
| Test results | `pdlf-outputs\f45\{slug}-f45-{run}-checks.xml` |
| Step Receipt | `pdlf-outputs\f45\{slug}-f45-{run}-receipt.md` |

All paths without a repository name are inside `{slug}-project-library\`.

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `45` |
| `step_type` | `skill` |
| `skill_family` | `gstack` |
| `run` | From the entry record |
| `ticket` | Empty |
| `app_number` | From the entry record |
| `status` | `complete` when the watch period passes |
| `synthesized` | `false` |
| `artifact_path` | `pdlf-outputs\f45\{slug}-f45-{run}-production.md` |
| `inputs_used` | Step 44 |
