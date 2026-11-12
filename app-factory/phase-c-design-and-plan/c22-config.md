---
title: "c22-config"
doc-id: "mb-6f917d23"
updated: "2026-11-12"
---
# Step 22 — Screen Requirements: Configuration

The fixed values of Step 22. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-c-design-and-plan/c22-reference|Step 22 Reference]]](C:/pdlf/app-factory/phase-c-design-and-plan/c22-reference.md). What the step is and why: [[[pdlf:app-factory/phase-c-design-and-plan/c22-explainer|Step 22 Explainer]]](C:/pdlf/app-factory/phase-c-design-and-plan/c22-explainer.md). What it must prove: [[[pdlf:app-factory/phase-c-design-and-plan/c22-test-spec|Step 22 Test Specification]]](C:/pdlf/app-factory/phase-c-design-and-plan/c22-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 22, Screen requirements |
| Phase | C, Design and Plan |
| Carried out by | OpenCode; David answers what the documents do not settle |
| Runs for | App 1 and App 5 as a whole application; every feature with forms |
| Previous step | 21 |
| Next step | 23 |
| Gate | None |
| BFT level | Full |
| Sentinel scrutiny | Low |
| Conditional | No |

## Inputs

| Input | Where |
|---|---|
| Tickets and ticket list | `{slug}-project-library\pdlf-tickets\{run}\`; `pdlf-outputs\c19\{slug}-c19-{run}-ticket-list.md` |
| Flows | `{slug}-project-library\pdlf-outputs\c19\` |
| Design system | `{slug}-project-library\docs-local\DESIGN.md` |
| Authoritative schema | `{slug}-project-library\docs-standard-local\authoritative-schema.md` |
| Access matrix | `{slug}-project-library\docs-local\design\app{n}\access-matrix.yaml` |
| Glossary | `{slug}-project-library\docs-local\GLOSSARY.md` |
| Model screen requirement | `{slug}-project-library\ui\(PACKAGE-NAME)\(FORM-NAME)\(FORM-NAME)-requirement.md` |
| Theme documentation | `C:\dev\dev-m3-custom-theme\m3-custom-theme-project-library\docs\`: `base-inventory.md`, `components\`, `usage-guide.md` |
| Allowed standard components | `approved_components` in `C:\dev\dev-{slug}\{slug}-app{n}\tests\ts-config.yaml` |
| UI rules | [[[default:specifications-global/spec-ui-standards\|UI Standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md); [[[default:specifications-global/mo-ui-production\|UI Production Method]]](C:/dev/project-library-global/specifications-global/mo-ui-production.md) |

## Component choice

| Element served by | Rule |
|---|---|
| A theme component that fits the element's purpose | The theme component that serves it best, with the reason it serves better than the other candidates |
| No theme component | An Anvil standard component in `approved_components`, with the reason no theme component serves |
| Neither | Stop and ask David; never a banned or unlisted component |

## Outputs

| Output | Where |
|---|---|
| Screen requirements | `ui\<package path>\<FormName>\<FormName>-requirement.md`, `status: draft` |
| Access matrix | `docs-local\design\app{n}\access-matrix.yaml`, `forms` entries added |
| Requirement index | `pdlf-outputs\c22\{slug}-c22-{run}-requirement-index.md`: every form by module path, its ticket, its requirement's path; and every existing form no ticket names |
| Test results | `pdlf-outputs\c22\{slug}-c22-{run}-checks.xml` |
| Step Receipt | `pdlf-outputs\c22\{slug}-c22-{run}-receipt.md` |
| Ledger | the Step 22 `steps` row; its BFT record; its `triage_findings` row |

All paths without a repository name are inside `{slug}-project-library\`.

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `22` |
| `step_type` | `skill` |
| `skill_family` | `opencode` |
| `run` | From the entry record |
| `app_number` | From the entry record |
| `status` | `complete` when every form the tickets name has its screen requirement |
| `synthesized` | `false` |
| `artifact_path` | `ui\` |
| `inputs_used` | Steps 19 to 21 |
