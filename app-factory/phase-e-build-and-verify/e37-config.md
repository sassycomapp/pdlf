---
title: "e37-config"
doc-id: "mb-c7c8ad61"
updated: "2026-11-13"
---
# Step 37 — Code Review: Configuration

The fixed values of Step 37. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-e-build-and-verify/e37-reference|Step 37 Reference]]](C:/pdlf/app-factory/phase-e-build-and-verify/e37-reference.md). What the step is and why: [[[pdlf:app-factory/phase-e-build-and-verify/e37-explainer|Step 37 Explainer]]](C:/pdlf/app-factory/phase-e-build-and-verify/e37-explainer.md). What it must prove: [[[pdlf:app-factory/phase-e-build-and-verify/e37-test-spec|Step 37 Test Specification]]](C:/pdlf/app-factory/phase-e-build-and-verify/e37-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 37, Code Review |
| Phase | E, Build and Verify |
| Carried out by | OpenCode, with the skills below, each in its own session |
| Runs for | Every ticket of the run, once each, in build order |
| Previous step | 36 |
| Next step | 38 |
| Gate | None |
| BFT level | Full |
| Sentinel scrutiny | Very High |
| Conditional | No |

## Inputs

| Input | Where |
|---|---|
| The feature's changes | `C:\dev\dev-{slug}\{slug}-app{n}`, since the previous ticket's gate commit |
| Ticket and test plan | `{slug}-project-library\pdlf-tickets\{run}\{ticket}.md`; `docs-local\design\{run}\test-plan.md` |
| Scaffold specification | `{slug}-project-library\docs-standard-local\scaffold-spec.md` |
| Approved screen requirements | `{slug}-project-library\ui\`, the ticket's forms |

## Review standards

| Standard | Covers |
|---|---|
| Anvil's `server-code`, `client-modules`, `client-forms`, `data-models`, `anvil-yaml` | How Anvil code, forms, data and settings are written |
| `spec-anvil-platform-standards` | Mybizz's Anvil patterns |
| `pol-common-aspects-for-mybizz-anvil-applications` | The aspects every app shares |
| `spec-ui-standards` and the approved screen requirements | The forms and spec sheets |
| The ticket | What the change must do |

## Outputs

| Output | Where |
|---|---|
| Findings | `pdlf-outputs\e37\{slug}-e37-{run}-{ticket}-findings.md`: each finding with its file, line and severity, or a clean-pass statement |
| Ledger | the Step 37 `steps` row for the ticket; its BFT record; its `triage_findings` row |
| Test results | `pdlf-outputs\e37\{slug}-e37-{run}-{ticket}-checks.xml` |
| Step Receipt | `pdlf-outputs\e37\{slug}-e37-{run}-{ticket}-receipt.md` |

All paths without a repository name are inside `{slug}-project-library\`.

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `37` |
| `step_type` | `skill` |
| `skill_family` | `matt-skills` |
| `run` | From the entry record |
| `ticket` | The ticket's slug |
| `app_number` | From the entry record |
| `status` | `complete` when every review has run |
| `synthesized` | `false` |
| `artifact_path` | `pdlf-outputs\e37\{slug}-e37-{run}-{ticket}-findings.md` |
| `inputs_used` | Step 36 |
