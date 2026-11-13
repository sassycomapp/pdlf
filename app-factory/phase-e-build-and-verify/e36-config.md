---
title: "e36-config"
doc-id: "mb-67e8bd49"
updated: "2026-11-13"
---
# Step 36 — Design Review: Configuration

The fixed values of Step 36. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-e-build-and-verify/e36-reference|Step 36 Reference]]](C:/pdlf/app-factory/phase-e-build-and-verify/e36-reference.md). What the step is and why: [[[pdlf:app-factory/phase-e-build-and-verify/e36-explainer|Step 36 Explainer]]](C:/pdlf/app-factory/phase-e-build-and-verify/e36-explainer.md). What it must prove: [[[pdlf:app-factory/phase-e-build-and-verify/e36-test-spec|Step 36 Test Specification]]](C:/pdlf/app-factory/phase-e-build-and-verify/e36-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 36, Design Review |
| Phase | E, Build and Verify |
| Carried out by | OpenCode, with `browse` |
| Runs for | Every ticket of the run, once each, in build order |
| Previous step | 40B |
| Next step | 37 |
| Gate | None |
| BFT level | Full |
| Sentinel scrutiny | None |
| Conditional | No |

## Inputs

| Input | Where |
|---|---|
| Approved screen requirements | `{slug}-project-library\ui\`, the ticket's forms |
| Design system | `{slug}-project-library\docs-local\DESIGN.md` |
| Theme inventory | `C:\dev\dev-{slug}\{slug}-app{n}\tests\component-inventory.yaml` |
| Hosted app | App {n}'s address, with a `TEST_` user for each role |

## Views

| Width | Mode | Roles |
|---|---|---|
| 390 px and 1440 px | Light and dark | Every role the access matrix lets use the form |

## Outputs

| Output | Where |
|---|---|
| Screenshots | `pdlf-outputs\e36\{slug}-e36-{run}-{ticket}-{form}-{width}-{mode}-{role}.png` |
| Findings | `pdlf-outputs\e36\{slug}-e36-{run}-{ticket}-findings.md`: each finding with its form, evidence and severity, or a clean-pass statement |
| Ledger | the Step 36 `steps` row for the ticket; its BFT record |
| Test results | `pdlf-outputs\e36\{slug}-e36-{run}-{ticket}-checks.xml` |
| Step Receipt | `pdlf-outputs\e36\{slug}-e36-{run}-{ticket}-receipt.md` |

All paths without a repository name are inside `{slug}-project-library\`.

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `36` |
| `step_type` | `skill` |
| `skill_family` | `gstack` |
| `run` | From the entry record |
| `ticket` | The ticket's slug |
| `app_number` | From the entry record |
| `status` | `complete` when every form is reviewed |
| `synthesized` | `false` |
| `artifact_path` | `pdlf-outputs\e36\{slug}-e36-{run}-{ticket}-findings.md` |
| `inputs_used` | Step 40B |
