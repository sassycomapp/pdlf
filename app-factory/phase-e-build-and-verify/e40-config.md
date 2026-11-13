---
title: "e40-config"
doc-id: "mb-8575eede"
updated: "2026-11-13"
---
# Step 40 — Architecture Scan: Configuration

The fixed values of Step 40. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-e-build-and-verify/e40-reference|Step 40 Reference]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40-reference.md). What the step is and why: [[[pdlf:app-factory/phase-e-build-and-verify/e40-explainer|Step 40 Explainer]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40-explainer.md). What it must prove: [[[pdlf:app-factory/phase-e-build-and-verify/e40-test-spec|Step 40 Test Specification]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 40, Architecture Scan |
| Phase | E, Build and Verify |
| Carried out by | OpenCode, with the skills below; David decides |
| Runs for | Every ticket of the run, once each, in build order |
| Previous step | 35A |
| Next step | 40B |
| Gate | None |
| BFT level | Light |
| Sentinel scrutiny | None |
| Conditional | Yes; David decides for each ticket whether it runs |

## Inputs

| Input | Where |
|---|---|
| Scaffold specification | `{slug}-project-library\docs-standard-local\scaffold-spec.md` |
| The app | `C:\dev\dev-{slug}\{slug}-app{n}` |

## Outputs

| Output | Where |
|---|---|
| Scan report | `pdlf-outputs\e40\{slug}-e40-{run}-{ticket}-scan.md`: each finding and David's decision |
| Ledger | the Step 40 `steps` row for the ticket; its BFT record |
| Test results | `pdlf-outputs\e40\{slug}-e40-{run}-{ticket}-checks.xml` |
| Step Receipt | `pdlf-outputs\e40\{slug}-e40-{run}-{ticket}-receipt.md` |

All paths without a repository name are inside `{slug}-project-library\`.

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `40` |
| `step_type` | `optional` |
| `skill_family` | `matt-skills` |
| `run` | From the entry record |
| `ticket` | The ticket's slug |
| `app_number` | From the entry record |
| `status` | `complete`, or `skipped` when David chooses not to run it |
| `synthesized` | `false` |
| `artifact_path` | `pdlf-outputs\e40\{slug}-e40-{run}-{ticket}-scan.md` |
| `inputs_used` | Step 35A |
