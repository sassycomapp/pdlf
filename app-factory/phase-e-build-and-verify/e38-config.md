---
title: "e38-config"
doc-id: "mb-eaf9d4db"
updated: "2026-11-13"
---
# Step 38 — Quality Testing: Configuration

The fixed values of Step 38. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-e-build-and-verify/e38-reference|Step 38 Reference]]](C:/pdlf/app-factory/phase-e-build-and-verify/e38-reference.md). What the step is and why: [[[pdlf:app-factory/phase-e-build-and-verify/e38-explainer|Step 38 Explainer]]](C:/pdlf/app-factory/phase-e-build-and-verify/e38-explainer.md). What it must prove: [[[pdlf:app-factory/phase-e-build-and-verify/e38-test-spec|Step 38 Test Specification]]](C:/pdlf/app-factory/phase-e-build-and-verify/e38-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 38, Quality Testing |
| Phase | E, Build and Verify |
| Carried out by | OpenCode, with the skills below |
| Runs for | Every ticket of the run, once each, in build order |
| Previous step | 37 |
| Next step | 38A |
| Gate | None |
| BFT level | Full |
| Sentinel scrutiny | High |
| Conditional | No; payments only when the feature touches them |

## Inputs

| Input | Where |
|---|---|
| Spec sheets | `C:\dev\dev-{slug}\{slug}-app{n}\theme\assets\docs\app{n}\`, the ticket's forms |
| Test plan | `{slug}-project-library\docs-local\design\{run}\test-plan.md` |
| Earlier features | Every ticket of the run with `build-verified` passed |
| Hosted app | App {n}'s address, with a `TEST_` user for each role |

## Outputs

| Output | Where |
|---|---|
| Findings | `pdlf-outputs\e38\{slug}-e38-{run}-{ticket}-findings.md`: each finding with its evidence and severity, or a clean-pass statement |
| Performance results | `pdlf-outputs\e38\{slug}-e38-{run}-{ticket}-benchmark.md` |
| Ledger | the Step 38 `steps` row for the ticket; its BFT record; its `triage_findings` row |
| Test results | `pdlf-outputs\e38\{slug}-e38-{run}-{ticket}-checks.xml` |
| Step Receipt | `pdlf-outputs\e38\{slug}-e38-{run}-{ticket}-receipt.md` |

All paths without a repository name are inside `{slug}-project-library\`.

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `38` |
| `step_type` | `skill` |
| `skill_family` | `gstack` |
| `run` | From the entry record |
| `ticket` | The ticket's slug |
| `app_number` | From the entry record |
| `status` | `complete` when every test has run |
| `synthesized` | `false` |
| `artifact_path` | `pdlf-outputs\e38\{slug}-e38-{run}-{ticket}-findings.md` |
| `inputs_used` | Step 37 |
