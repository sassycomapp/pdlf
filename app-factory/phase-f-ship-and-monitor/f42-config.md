---
title: "f42-config"
doc-id: "mb-ae23ef5b"
updated: "2026-11-13"
---
# Step 42 — Release to App 2: Configuration

The fixed values of Step 42. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-f-ship-and-monitor/f42-reference|Step 42 Reference]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f42-reference.md). What the step is and why: [[[pdlf:app-factory/phase-f-ship-and-monitor/f42-explainer|Step 42 Explainer]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f42-explainer.md). What it must prove: [[[pdlf:app-factory/phase-f-ship-and-monitor/f42-test-spec|Step 42 Test Specification]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f42-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 42, Release to App 2 |
| Phase | F, Ship and Monitor |
| Carried out by | David, with `wizard` instructions; OpenCode checks |
| Runs for | App 1 and App 5 runs, and every release |
| Previous step | 41 |
| Next step | 42A |
| Gate | None |
| BFT level | Light |
| Sentinel scrutiny | None |
| Conditional | Skipped for an App 5 run |

## Inputs

| Input | Where |
|---|---|
| Release tag | App 1's tag from Step 41 |
| Migration plan | `{slug}-project-library\docs-local\schema-migration-log.md` |
| App 2, App 3, App 4 | `C:\dev\dev-{slug}\{slug}-app2`, `{slug}-app3`, `{slug}-app4` |

## Order of work

| # | Work | Check |
|---|---|---|
| 1 | Every client instance backs up to its own bucket | RL-02 |
| 2 | App 1's tag pushed into App 2 | App 2 equals the tag |
| 3 | Table changes written into App 3 | RL-03 |
| 4 | The image built, scanned and signed by the `{slug}-app4` workflow | No end-of-life software; no high or critical finding older than 14 days |
| 5 | The suite runs on the image | PR-08 |
| 6 | App 5 moves the test client instance to the image by digest | RL-04, RL-05, RL-19 |

## Outputs

| Output | Where |
|---|---|
| Image record | `pdlf-outputs\f42\{slug}-f42-{run}-image.md`: the tag, digest, scan result and signature |
| Ledger | the Step 42 `steps` row; its BFT record |
| Test results | `pdlf-outputs\f42\{slug}-f42-{run}-checks.xml` |
| Step Receipt | `pdlf-outputs\f42\{slug}-f42-{run}-receipt.md` |

All paths without a repository name are inside `{slug}-project-library\`.

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `42` |
| `step_type` | `manual` |
| `skill_family` | `manual` |
| `run` | From the entry record |
| `ticket` | Empty |
| `app_number` | From the entry record |
| `status` | `complete` when the test client instance runs the image; `skipped` for App 5 |
| `synthesized` | `false` |
| `artifact_path` | `pdlf-outputs\f42\{slug}-f42-{run}-image.md` |
| `inputs_used` | Step 41 |
