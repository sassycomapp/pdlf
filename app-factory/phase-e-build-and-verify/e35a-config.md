---
title: "e35a-config"
doc-id: "mb-b18165ee"
updated: "2026-11-13"
---
# Step 35A — Testing: Configuration

The fixed values of Step 35A. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-e-build-and-verify/e35a-reference|Step 35A Reference]]](C:/pdlf/app-factory/phase-e-build-and-verify/e35a-reference.md). What the step is and why: [[[pdlf:app-factory/phase-e-build-and-verify/e35a-explainer|Step 35A Explainer]]](C:/pdlf/app-factory/phase-e-build-and-verify/e35a-explainer.md). What it must prove: [[[pdlf:app-factory/phase-e-build-and-verify/e35a-test-spec|Step 35A Test Specification]]](C:/pdlf/app-factory/phase-e-build-and-verify/e35a-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 35A, Testing |
| Phase | E, Build and Verify |
| Carried out by | OpenCode, with the skills below |
| Runs for | Every ticket of the run, once each, in build order |
| Previous step | 35 |
| Next step | 40 |
| Gate | None |
| BFT level | Light |
| Sentinel scrutiny | None |
| Conditional | No |

## Inputs

| Input | Where |
|---|---|
| Ticket | `{slug}-project-library\pdlf-tickets\{run}\{ticket}.md` |
| Test plan | `{slug}-project-library\docs-local\design\{run}\test-plan.md` |
| The app and its tests | `C:\dev\dev-{slug}\{slug}-app{n}`; `tests\` |

## Outputs

| Output | Where |
|---|---|
| Added tests | `{slug}-app{n}\tests\` |
| Test audit | `pdlf-outputs\e35a\{slug}-e35a-{run}-{ticket}-test-audit.md` |
| Ledger | the Step 35A `steps` row for the ticket; its BFT record |
| Test results | `pdlf-outputs\e35a\{slug}-e35a-{run}-{ticket}-checks.xml` |
| Step Receipt | `pdlf-outputs\e35a\{slug}-e35a-{run}-{ticket}-receipt.md` |

All paths without a repository name are inside `{slug}-project-library\`.

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `35A` |
| `step_type` | `skill` |
| `skill_family` | `matt-skills` |
| `run` | From the entry record |
| `ticket` | The ticket's slug |
| `app_number` | From the entry record |
| `status` | `complete` when every added test passes |
| `synthesized` | `false` |
| `artifact_path` | `{slug}-app{n}\tests\` |
| `inputs_used` | Step 35 |
