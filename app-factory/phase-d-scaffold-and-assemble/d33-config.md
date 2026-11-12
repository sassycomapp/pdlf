---
title: "d33-config"
doc-id: "mb-273c04d9"
updated: "2026-11-12"
---
# Step 33 — Pull to Local: Configuration

The fixed values of Step 33. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d33-reference|Step 33 Reference]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d33-reference.md). What the step is and why: [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d33-explainer|Step 33 Explainer]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d33-explainer.md). What it must prove: [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d33-test-spec|Step 33 Test Specification]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d33-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 33, Pull to local |
| Phase | D, Scaffold and Assemble |
| Carried out by | David runs the pull; OpenCode checks it |
| Runs for | Every run that reached Step 32 |
| Previous step | 32 |
| Next step | 34 |
| Gate | None |
| BFT level | None |
| Sentinel scrutiny | None |
| Conditional | No |

## The procedure

| Item | Value |
|---|---|
| Procedure, command and checks | Step 18's, in [[[pdlf:app-factory/phase-c-design-and-plan/c18-config\|Step 18 Configuration]]](C:/pdlf/app-factory/phase-c-design-and-plan/c18-config.md) |
| Expected change | Every module and function on `pdlf-outputs\d32\{slug}-d32-{run}-stubs.md`, and `tests\ts-config.yaml` |

## Outputs

| Output | Where |
|---|---|
| Test results | `pdlf-outputs\d33\{slug}-d33-{run}-checks.xml` |
| Step Receipt | `pdlf-outputs\d33\{slug}-d33-{run}-receipt.md`, recording the commit `master` now points to |
| Ledger | the Step 33 `steps` row |

All paths are inside `{slug}-project-library\`.

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `33` |
| `step_type` | `manual` |
| `skill_family` | `manual` |
| `run` | From the entry record |
| `app_number` | From the entry record |
| `status` | `complete` when every check passes |
| `synthesized` | `false` |
| `artifact_path` | `{slug}-app{n}` |
| `inputs_used` | Step 32 |
