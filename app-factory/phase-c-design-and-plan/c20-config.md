---
title: "c20-config"
doc-id: "mb-47b5f04b"
updated: "2026-11-12"
---
# Step 20 — Design System: Configuration

The fixed values of Step 20. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-c-design-and-plan/c20-reference|Step 20 Reference]]](C:/pdlf/app-factory/phase-c-design-and-plan/c20-reference.md). What the step is and why: [[[pdlf:app-factory/phase-c-design-and-plan/c20-explainer|Step 20 Explainer]]](C:/pdlf/app-factory/phase-c-design-and-plan/c20-explainer.md). What it must prove: [[[pdlf:app-factory/phase-c-design-and-plan/c20-test-spec|Step 20 Test Specification]]](C:/pdlf/app-factory/phase-c-design-and-plan/c20-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 20, Design system |
| Phase | C, Design and Plan |
| Carried out by | OpenCode, with the skills below; David approves `DESIGN.md` |
| Runs for | App 1 and App 5 as a whole application; a feature only when it changes the design system |
| Previous step | 19 |
| Next step | 21 |
| Gate | None |
| BFT level | Full |
| Sentinel scrutiny | Medium |
| Conditional | In a test run, David may abbreviate or skip it |

## Inputs

| Input | Where |
|---|---|
| Reviewed plan | `{slug}-project-library\docs-local\design\{run}\design-doc.md` |
| Glossary | `{slug}-project-library\docs-local\GLOSSARY.md` |
| Ticket list | `{slug}-project-library\pdlf-outputs\c19\{slug}-c19-{run}-ticket-list.md` |
| Brand material | `{slug}-project-library\assets-local\` |
| Existing design system | `{slug}-project-library\docs-local\DESIGN.md` |
| Theme guide and inventory | `C:\dev\dev-m3-custom-theme\m3-custom-theme-project-library\docs\` |
| UI rules | [[[default:specifications-global/spec-ui-standards\|UI Standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md) |
| Context pack | [[[pdlf:pdlf-library/specifications-local/spec-skill-context-pack\|Spec: Skill Context Pack]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-context-pack.md) |

## Choices `DESIGN.md` records

| Choice | Allowed values |
|---|---|
| Starting palette | `default`, `professional_blue`, `warm_coral`, `calm_teal`, `sophisticated_purple`, `sky_blue`, `forest_green`, `desert_rose` |
| Starting mode | `light`, `dark` or `system` |
| User choice | Whether users may change palette and mode |
| Menu style | `baseline`, `standard` or `vibrant` |
| Logo and imagery | Files in `assets-local\` |
| Tone of text | A short statement, for the English phrase texts |

## Fixed statements in `DESIGN.md`

| Statement | Source |
|---|---|
| Every form meets `spec-ui-standards` | `spec-ui-standards` |
| Every element uses the theme component that serves it best, chosen from the whole inventory | `spec-ui-standards` section 3 |
| Not used: `Label`, `HtmlTemplate`, `HtmlPanel`, Anvil Extras, any component outside the theme and `approved_components` | `spec-ui-standards` section 3 |

## Outputs

| Output | Where |
|---|---|
| Design system | `docs-local\DESIGN.md` |
| Step-folder copy | `pdlf-outputs\c20\{slug}-c20-{run}-design.md` |
| Test results | `pdlf-outputs\c20\{slug}-c20-{run}-checks.xml` |
| Step Receipt | `pdlf-outputs\c20\{slug}-c20-{run}-receipt.md` |
| Ledger | the Step 20 `steps` row; its BFT record; its `triage_findings` row |

All paths without a repository name are inside `{slug}-project-library\`.

## Fixed answers for `/design-consultation`

| Question or default in the skill | Answer |
|---|---|
| Where to write `DESIGN.md` | `docs-local\DESIGN.md` in the project library |
| Colours, fonts, sizes, spacing | Never defined; chosen only from the theme's options above |
| Preview page | Not written; the theme's demo form shows every token |

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `20` |
| `step_type` | `skill` |
| `skill_family` | `gstack` |
| `run` | From the entry record |
| `app_number` | From the entry record |
| `status` | `complete` after David approves `DESIGN.md`; `skipped` when David skips it in a test run |
| `synthesized` | `false` |
| `artifact_path` | `docs-local\DESIGN.md` |
| `inputs_used` | Step 19 |
