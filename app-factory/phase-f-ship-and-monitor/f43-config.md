---
title: "f43-config"
doc-id: "mb-c55a9572"
updated: "2026-11-13"
---
# Step 43 — Client Instance Check: Configuration

The fixed values of Step 43. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-f-ship-and-monitor/f43-reference|Step 43 Reference]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f43-reference.md). What the step is and why: [[[pdlf:app-factory/phase-f-ship-and-monitor/f43-explainer|Step 43 Explainer]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f43-explainer.md). What it must prove: [[[pdlf:app-factory/phase-f-ship-and-monitor/f43-test-spec|Step 43 Test Specification]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f43-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 43, Client Instance Check |
| Phase | F, Ship and Monitor |
| Carried out by | OpenCode, with the skills below |
| Runs for | App 1 and App 5 runs, and every release |
| Previous step | 42A |
| Next step | 44 |
| Gate | None |
| BFT level | Light |
| Sentinel scrutiny | None |
| Conditional | Skipped for an App 5 run; RL-10 only at a first release |

## Inputs

| Input | Where |
|---|---|
| Test client instance | Its address and heartbeat in App 5 |
| Hosting specification | `spec-client-instance-hosting` |

## Outputs

| Output | Where |
|---|---|
| Results | `pdlf-outputs\f43\{slug}-f43-{run}-results.md`: smoke test, heartbeat, RL-10, SC-14 |
| Health baseline | `pdlf-outputs\f43\{slug}-f43-{run}-baseline.md` |
| Ledger | the Step 43 `steps` row; its BFT record |
| Test results | `pdlf-outputs\f43\{slug}-f43-{run}-checks.xml` |
| Step Receipt | `pdlf-outputs\f43\{slug}-f43-{run}-receipt.md` |

All paths without a repository name are inside `{slug}-project-library\`.

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `43` |
| `step_type` | `skill` |
| `skill_family` | `gstack` |
| `run` | From the entry record |
| `ticket` | Empty |
| `app_number` | From the entry record |
| `status` | `complete` when every check passes; `skipped` for App 5 |
| `synthesized` | `false` |
| `artifact_path` | `pdlf-outputs\f43\{slug}-f43-{run}-results.md` |
| `inputs_used` | Step 42A |
