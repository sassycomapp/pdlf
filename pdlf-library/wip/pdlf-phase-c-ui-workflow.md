---
title: "pdlf-phase-c-ui-workflow"
doc-id: "mb-a9bcf67f"
updated: "2026-11-06"
---
# PDLF Phase C — UI Workflow

## 1. What This Document Is

- This document is the plan that brings the UI production system into PDLF, `project-library-global`, the project template and the mb-3-cs run.
- The system itself is defined by two global documents:
  - [[[default:specifications-global/spec-ui-standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md): the rules every form meets;
  - [[[default:specifications-global/mo-ui-production]]](C:/dev/project-library-global/specifications-global/mo-ui-production.md): the method that produces the forms, feature by feature.
- Every user interface is built on `m3-custom-theme`, package name `m3`, which entirely replaces Anvil's M3 Theme (app `4UK6WHQ6UX7AKELK`).
- `m3-custom-theme` is partly built. Every task that needs the finished theme waits for it (section 4, batch 5).

## 2. Established Facts

### 2.1 Anvil Forms

- An Anvil form is two files: `form_template.html` (or legacy `form_template.yaml`) and `__init__.py`.
- An HTML form template names each component by type path and sets its properties as `prop:<name>`. Anvil draws the form from the file, and the form stays editable in the designer.
- Forms using `m3._Components` tags display only inside Anvil.
- Anvil's agent rules treat YAML forms as legacy. `anvil convert-template` converts them to HTML.
- App 1 holds 93 forms: 91 YAML and 2 HTML. The 91 YAML forms refer to the theme by dependency ID (306 references), so they stop loading when the dependency is swapped. Every one of them is replaced.
- App 1's shared code imports `m3.components`, which keeps working under the package name `m3`.
- App 1 starts on `auth.LoginForm` and uses the `routing` dependency.

### 2.2 Anvil Agent

- The Anvil agent runs in the Anvil editor on the AI account David connects. With his Claude account connected, the agent is Claude.
- The agent reads and edits forms, client code, server code and theme files, including `theme/assets/`.
- The agent commits automatically to `master`.
- The agent cannot change Data Tables.
- The agent's rules forbid guessing dependency component properties. Its references cover only Anvil's base M3 theme.
- The agent's `/review-commit` command reviews the changes in a commit.

### 2.3 Anvil CLI

- David's computer has Anvil CLI 0.7.7. The CLI is updated only when David decides.
- `anvil validate <path>` checks `anvil.yaml`, YAML, HTML and Python files under `client_code` and `server_code`, with or without logging in.
- Tested with 0.7.7: Python errors are caught; unclosed HTML tags, unknown component types and unknown properties are not caught.
- The CLI's `watch` command is not used. App 1 syncs between Anvil and GitHub, and David pulls and pushes with `git pull` and `gcp`.

### 2.4 Test Suite

- `ts_scan.py` reads only `form_template.yaml` files, so its form checks (ST-11 approved components, banned components, colour values) see no HTML form.
- `ts_scan.py` bans `SidesheetContent`, which `spec-component-properties.md` approves.
- The access-matrix template keys forms by bare name. BR-03 reads those keys.
- ST-14 requires every visible text to be a phrase key.

### 2.5 Writeback (Anvil's Base M3 Theme Source)

- TextBox and TextArea: `text`. Checkbox: `checked`. Switch: `selected`. RadioGroupPanel and DropdownMenu: `selected_value`. Slider: `value`.

## 3. Order of Precedence

| # | Task | Waits for |
|---|---|---|
| 1 | Deliver batch 1 | — |
| 2 | Migrate `mb-3-cs-project-context` into `mb-3-cs-project-library` (batch 2) | 1 |
| 3 | Align the global UI documents and remove the obsolete ones (batch 3) | 2 |
| 4 | Restructure the `ui` folders and the access-matrix template (batch 4) | 3 |
| 5 | Finish `m3-custom-theme`, including its component documentation | — |
| 6 | Theme-dependent work: test suite, nomenclature, component properties, `mb-form-builder`, PDLF steps (batch 5) | 4, 5 |
| 7 | Swap App 1's dependency to `m3-custom-theme`; check that `4UK6WHQ6UX7AKELK` is gone from `anvil.yaml` | 5 |
| 8 | Prove `anvil validate` on David's computer with one form | 7 |
| 9 | Test `mb-form-builder` on one form; David approves the form in Anvil | 6, 8 |
| 10 | Run [[[default:specifications-global/mo-ui-production]]](C:/dev/project-library-global/specifications-global/mo-ui-production.md) feature by feature: `layouts` and `shared`, then `auth`, then the rest | 9 |

## 4. Batches

### Batch 1 — Core Documents

| File | Path | Change |
|---|---|---|
| `spec-ui-standards.md` | `C:\dev\project-library-global\specifications-global\` | Replaced: the UI rules of this system |
| `mo-ui-production.md` | `C:\dev\project-library-global\specifications-global\` | New: the method of this system |
| `pdlf-phase-c-ui-workflow.md` | `C:\pdlf\pdlf-library\wip\` | New: this plan |
| `commands.md` | `C:\dev\project-library-global\anvil-docs\using-another-ide\` | Replaced: `validate` covers YAML, HTML and Python files and folders, with its tested limits |

### Batch 2 — Project Library Migration

- A job of its own, scoped with David before any file moves.
- Every file in `mb-3-cs-project-context` moves to its place in `mb-3-cs-project-library`, keeping every link and reference intact.
- Each move is checked with a read-only command first. Nothing is deleted until its copy is confirmed in place.

### Batch 3 — Global UI Documents

| File | Change |
|---|---|
| `adr-htmltemplate-use.md` | States the ban for `m3-custom-theme`; states that HTML form templates are not `HtmlTemplate` |
| `adr-role-property-assignment-mechanism.md` | Roles are set in the form template (`prop:role`) |
| `adr-dark-mode.md` | Dark mode comes from the theme's palettes; forms hold no colour scheme |
| `adr-ui-customization-approach.md` | Customisation lives in `m3-custom-theme` |
| `adr-responsive-behaviour-mechanism.md` | "Wireframe" becomes "screen requirement" |
| `spec-anvil-platform-standards.md` | Section 1: HTML form templates. Section 4: writeback is set in the form template. Section 9: replaced by a link to [[[default:specifications-global/mo-ui-production]]](C:/dev/project-library-global/specifications-global/mo-ui-production.md) |
| `pol-common-aspects-for-mybizz-anvil-applications.md`, `spec-nomenclature.md`, `ts-catalogue.md`, `ts-conformance-checks.md` | Links to the seven removed files point to [[[default:specifications-global/spec-ui-standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md) |
| `c20-build-plan.md`, `c22-build-plan.md`, `c27-build-plan.md`, `d29-build-plan.md`, `spec-skill-context-pack.md`, `pdlf-pass2-demand-map.md` (PDLF) | Links to the seven removed files point to [[[default:specifications-global/spec-ui-standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md) |
| `design-doc.md`, `design-doc-first-concept.md`, `mb-3-cs-b12-app1-design-doc.md`, `mb-3-cs-b12-app1-design-doc-first-concept.md`, `mb-3-cs-b14-app1-receipt.md`, `mb-3-cs-b14-app1-reviewed-plan.md` (mb-3-cs project library) | Links to the seven removed files point to [[[default:specifications-global/spec-ui-standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md) |
| `spec-m3_component_mapping.md`, `spec-m3-design-standards.md`, `spec-material-3-theme.md`, `spec-screen-production-standard.md`, `spec-screen-and-wireframe-production-standards.md`, `adr-material-3-theme-component-scope.md`, `adr-design-rules.md` | Removed, after every link above is repaired |
| `anvil-ui-build-standard.md` (project template and mb-3-cs project library) | Removed: replaced by [[[default:specifications-global/spec-ui-standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md) and the screen requirements |

### Batch 4 — UI Folders and Access Matrix

| File | Change |
|---|---|
| `ui\README.md` (project template and mb-3-cs project library) | One folder per `client_code` package path; one file per form, `<FormName>-requirement.md` |
| `ui\(PACKAGE-NAME)\(FORM-NAME)\` (project template and mb-3-cs project library) | The six wireframe and screen files are removed; `(FORM-NAME)-requirement.md` is added as the model |
| `test-suite\templates\access-matrix.yaml` | Forms keyed by module path |
| `spec-nomenclature.md` section 1.7 | One file per form folder, `<FormName>-requirement.md` |

### Batch 5 — After `m3-custom-theme` Is Finished

| File | Change |
|---|---|
| `test-suite\tools\ts_scan.py` | Reads `form_template.html`; checks component types and properties against the theme's documentation; checks closed tags; `SidesheetContent` unbanned |
| `test-suite\templates\ts-config.yaml` | `approved_components` holds only the Anvil standard components the theme has no counterpart for |
| `spec-component-properties.md` | Rebuilt from the theme's documentation |
| `spec-nomenclature.md` | Prefixes for every theme component; the event handler rule |
| `mb-form-builder` skill | Written to [[[default:specifications-global/mo-ui-production]]](C:/dev/project-library-global/specifications-global/mo-ui-production.md) section 5, installed, then documented with `mb-sysdoc-creator` and `mb-config-manager` |
| `skills-catalog.md` | `mb-form-builder` registered; the Magdoub wireframe skill removed from Phase C |
| PDLF steps C17 to C28 | Rebuilt to [[[default:specifications-global/mo-ui-production]]](C:/dev/project-library-global/specifications-global/mo-ui-production.md): screen requirements are written and approved in Phase C; forms are built per feature after the server code |
| `wireframe\` folder, with its rows in `README.md` and `AGENTS.md` (project template and mb-3-cs project library) | Removed, together with the Phase C rebuild, because no step writes wireframes |

## 5. References

| Source | Location |
|---|---|
| Anvil AI agent | https://anvil.works/docs/ai |
| Anvil AI agent launch | https://anvil.works/blog/ai-in-anvil |
| Anvil CLI commands | https://anvil.works/docs/using-another-ide/commands.html |
| Anvil agent form rules | `anvil-works/anvil-agent-references/skills/client-forms/SKILL.md` |
| Anvil agent dependency components | `anvil-works/anvil-agent-references/skills/client-forms/examples/dependency-component.md` |
| Anvil dependencies | `project-library-global/anvil-docs/deployment/dependencies.md` |
| Anvil navigation | `project-library-global/anvil-docs/client/navigation/_index.md` |
| Theme build | `m3-custom-theme-project-library/m3-custom-theme.md` |
| Theme components | `m3-custom-theme-project-library/docs/base-inventory.md`, `m3-custom-theme-project-library/docs/components/` |
| Test suite scanner | `project-library-global/test-suite/tools/ts_scan.py` |
| Document identity and links | [[[default:adr-global/adr-document-frontmatter-and-identity]]](C:/dev/project-library-global/adr-global/adr-document-frontmatter-and-identity.md) |
