---
title: "c23-config"
doc-id: "mb-1cbe5e07"
updated: "2026-11-12"
---
# Step 23 — Design Review: Configuration

The fixed values of Step 23. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-c-design-and-plan/c23-reference|Step 23 Reference]]](C:/pdlf/app-factory/phase-c-design-and-plan/c23-reference.md). What the step is and why: [[[pdlf:app-factory/phase-c-design-and-plan/c23-explainer|Step 23 Explainer]]](C:/pdlf/app-factory/phase-c-design-and-plan/c23-explainer.md). What it must prove: [[[pdlf:app-factory/phase-c-design-and-plan/c23-test-spec|Step 23 Test Specification]]](C:/pdlf/app-factory/phase-c-design-and-plan/c23-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 23, Design review |
| Phase | C, Design and Plan |
| Carried out by | OpenCode, with `/plan-design-review` |
| Runs for | Every run that reached Step 22 |
| Previous step | 22 |
| Next step | 26 (Steps 24 and 25 are not used) |
| Gate | None |
| BFT level | Full |
| Sentinel scrutiny | None; Step 22's review covers the same documents |
| Conditional | No |

## Inputs

| Input | Where |
|---|---|
| Screen requirements and index | `{slug}-project-library\ui\`; `pdlf-outputs\c22\{slug}-c22-{run}-requirement-index.md` |
| Design system | `{slug}-project-library\docs-local\DESIGN.md` |
| Tickets and flows | `{slug}-project-library\pdlf-tickets\{run}\`; `pdlf-outputs\c19\` |
| Theme documentation | `C:\dev\dev-m3-custom-theme\m3-custom-theme-project-library\docs\` |
| UI rules | [[[default:specifications-global/spec-ui-standards\|UI Standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md) |

## Reviews

| Review | By | Covers |
|---|---|---|
| Usability | `/plan-design-review` | Each design dimension the skill rates |
| Theme usage | OpenCode | Every element against the whole inventory |
| Accessibility | OpenCode | `spec-ui-standards` section 13 |
| Always-available controls | OpenCode | `spec-ui-standards` section 12 |

## Severity

| Severity | When |
|---|---|
| High | A theme-usage finding; a broken rule of `spec-ui-standards`; a flow that cannot be completed |
| Medium | A usability gap that slows or confuses the user |
| Low | A refinement |

## Outputs

| Output | Where |
|---|---|
| Design review | `pdlf-outputs\c23\{slug}-c23-{run}-design-review.md`: each finding with its requirement, element, proposed correction and severity; the skill's ratings |
| Test results | `pdlf-outputs\c23\{slug}-c23-{run}-checks.xml` |
| Step Receipt | `pdlf-outputs\c23\{slug}-c23-{run}-receipt.md` |
| Ledger | the Step 23 `steps` row; its BFT record |

All paths without a repository name are inside `{slug}-project-library\`.

## Fixed answers for `/plan-design-review`

| Question or default in the skill | Answer |
|---|---|
| What to review | The screen requirements and `DESIGN.md` |
| Edits to the plan | None; findings only, written to the design review |

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `23` |
| `step_type` | `skill` |
| `skill_family` | `gstack` |
| `run` | From the entry record |
| `app_number` | From the entry record |
| `status` | `complete` when every screen requirement is reviewed |
| `synthesized` | `false` |
| `artifact_path` | `pdlf-outputs\c23\{slug}-c23-{run}-design-review.md` |
| `inputs_used` | Step 22 |
