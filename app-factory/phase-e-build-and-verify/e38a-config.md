---
title: "e38a-config"
doc-id: "mb-fe48d787"
updated: "2026-11-13"
---
# Step 38A — Package Check: Configuration

The fixed values of Step 38A. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-e-build-and-verify/e38a-reference|Step 38A Reference]]](C:/pdlf/app-factory/phase-e-build-and-verify/e38a-reference.md). What the step is and why: [[[pdlf:app-factory/phase-e-build-and-verify/e38a-explainer|Step 38A Explainer]]](C:/pdlf/app-factory/phase-e-build-and-verify/e38a-explainer.md). What it must prove: [[[pdlf:app-factory/phase-e-build-and-verify/e38a-test-spec|Step 38A Test Specification]]](C:/pdlf/app-factory/phase-e-build-and-verify/e38a-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 38A, Package Check |
| Phase | E, Build and Verify |
| Carried out by | OpenCode; David copies Anvil's report |
| Runs for | Every ticket of the run, once each, in build order |
| Previous step | 38 |
| Next step | 39 |
| Gate | None |
| BFT level | None |
| Sentinel scrutiny | None |
| Conditional | Yes; skipped when the feature did not rebuild the server environment |

## Inputs

| Input | Where |
|---|---|
| Anvil's package report | The app's server environment settings in the Anvil editor |
| Step 35A's `pip-audit` result | `{slug}-project-library\pdlf-outputs\e35a\` |

## Outputs

| Output | Where |
|---|---|
| Package report | `pdlf-outputs\e38a\{slug}-e38a-{run}-{ticket}-packages.md` |
| Ledger | the Step 38A `steps` row for the ticket |
| Test results | `pdlf-outputs\e38a\{slug}-e38a-{run}-{ticket}-checks.xml` |
| Step Receipt | `pdlf-outputs\e38a\{slug}-e38a-{run}-{ticket}-receipt.md` |

All paths without a repository name are inside `{slug}-project-library\`.

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `38A` |
| `step_type` | `manual` |
| `skill_family` | `manual` |
| `run` | From the entry record |
| `ticket` | The ticket's slug |
| `app_number` | From the entry record |
| `status` | `complete`, or `skipped` when the server environment was not rebuilt |
| `synthesized` | `false` |
| `artifact_path` | `pdlf-outputs\e38a\{slug}-e38a-{run}-{ticket}-packages.md` |
| `inputs_used` | Step 38 |
