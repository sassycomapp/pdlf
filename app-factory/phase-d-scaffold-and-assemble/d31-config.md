---
title: "d31-config"
doc-id: "mb-d8224bb4"
updated: "2026-11-12"
---
# Step 31 — Scaffold Plan: Configuration

The fixed values of Step 31. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d31-reference|Step 31 Reference]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d31-reference.md). What the step is and why: [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d31-explainer|Step 31 Explainer]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d31-explainer.md). What it must prove: [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d31-test-spec|Step 31 Test Specification]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d31-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 31, Scaffold plan |
| Phase | D, Scaffold and Assemble; the first step of the phase |
| Carried out by | OpenCode, with the skills below; David approves `scaffold-spec.md` |
| Runs for | App 1 and App 5 as a whole application; every feature |
| Previous step | 26 (Steps 27 to 30 are not used) |
| Next step | 32 |
| Gate | None |
| BFT level | Full |
| Sentinel scrutiny | None; Step 34 reviews the structure at Very High |
| Conditional | No; `graphify` and the disposition list only for an existing app |

## Inputs

| Input | Where |
|---|---|
| Reviewed plan, with architecture and data design | `{slug}-project-library\docs-local\design\{run}\design-doc.md` |
| Test plan | `{slug}-project-library\docs-local\design\{run}\test-plan.md` |
| Glossary and ADRs | `{slug}-project-library\docs-local\GLOSSARY.md`; `adr-local\` |
| Access matrix and threat model | `{slug}-project-library\docs-local\design\app{n}\` |
| Tickets | `{slug}-project-library\pdlf-tickets\{run}\` |
| Approved screen requirements and index | `{slug}-project-library\ui\`; `pdlf-outputs\c22\{slug}-c22-{run}-requirement-index.md` |
| Authoritative schema | `{slug}-project-library\docs-standard-local\authoritative-schema.md` |
| Scaffold specification | `{slug}-project-library\docs-standard-local\scaffold-spec.md` |
| Existing app code | `C:\dev\dev-{slug}\{slug}-app{n}\client_code\`, `server_code\` |
| Scanner settings template | `C:\dev\project-library-global\test-suite\templates\ts-config.yaml` |
| Context pack | [[[pdlf:pdlf-library/specifications-local/spec-skill-context-pack\|Spec: Skill Context Pack]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-context-pack.md) |

## `scaffold-spec.md` sections

| Section | Holds |
|---|---|
| Package Structure | Every client and server module, by package, with its role and its functions |
| Custom Component Conventions | Every shared custom component, its module and the forms that use it |
| Database Schema | A pointer to `authoritative-schema.md`, and which behaviour lives on model classes, server methods or plain functions |
| M3 Component Standards | A pointer to `spec-ui-standards` and `DESIGN.md` |
| Navigation Architecture | The layouts, their menus and the forms each opens; public routes |
| Startup Configuration | The startup form or module, and the app's service settings |
| Dependencies | `m3-custom-theme` and Routing, by app ID |

## Planned function

| Field | Value |
|---|---|
| Name | As the screen requirement or ticket names it |
| Module | The module of the ticket's feature |
| Access | The decorator from the access matrix, or the reason it is public |
| Rate limit | For a public function or endpoint |
| Behaviour | One sentence |
| Test | The test plan's ID that proves it |

## Outputs

| Output | Where |
|---|---|
| Scaffold specification | `docs-standard-local\scaffold-spec.md` |
| Scanner settings | `pdlf-outputs\d31\{slug}-d31-{run}-scanner-settings.yaml`: the values for `tests\ts-config.yaml` |
| Module disposition list, existing app | `pdlf-outputs\d31\{slug}-d31-{run}-disposition.md`: every existing module and server function, keep, rework or remove, with its ticket |
| Step-folder copy | `pdlf-outputs\d31\{slug}-d31-{run}-scaffold-spec.md` |
| Test results | `pdlf-outputs\d31\{slug}-d31-{run}-checks.xml` |
| Step Receipt | `pdlf-outputs\d31\{slug}-d31-{run}-receipt.md` |
| Ledger | the Step 31 `steps` row; its BFT record |

All paths without a repository name are inside `{slug}-project-library\`.

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `31` |
| `step_type` | `skill` |
| `skill_family` | `matt-skills` |
| `run` | From the entry record |
| `app_number` | From the entry record |
| `status` | `complete` after David approves `scaffold-spec.md` |
| `synthesized` | `false` |
| `artifact_path` | `docs-standard-local\scaffold-spec.md` |
| `inputs_used` | Step 26 |
