---
title: "spec-nomenclature"
doc-id: "mb-f3c916b1"
updated: "2026-10-09"
---
# PDLF Nomenclature & Naming Conventions

**Authority:** Mandatory. Every PDLF step file, policy, and specification follows this
file. Any naming or path convention agreed in discussion is codified here before being
relied on elsewhere — this file is the single source of truth, not the discussion that
produced it.

---

## Acronyms

| Acronym | Meaning |
|---|---|
| PDLF | Project Development Lifecycle Framework |
| BFT | BODY Frame Thinking (de Bono) |
| ISA | Ideal State Artifact |
| ISC | Ideal State Criterion |
| ADR | Architecture Decision Record |
| PCD | Project Concept Document |
| PRD | Product Requirements Document |
| M3 / MD3 | Material Design 3 |
| GBrain | GBrain (memory layer, PGlite) |
| GStack | GStack (workflow layer, skills) |
| UAT | User Acceptance Testing |
| TDD | Test-Driven Development |
| NFR | Non-Functional Requirement |
| FS | Functional Specification |
| US | User Story |
| AC | Acceptance Criterion |
| RLS | Row-Level Security |
| CRM | Customer Relationship Management |
| DX | Developer Experience |
| VC | Version Control |
| WSL | Windows Subsystem for Linux |
| MCP | Model Context Protocol |
| TTHW | Time to Hello World (DX metric — time from install to first working output) |
| DA | Digital Assistant (LifeOS concept — the primary AI interface to a system) |

---

## Repo & Path Conventions

| Element | Convention | Example | Notes |
|---|---|---|---|
| Code repo (shorthand) | `{slug}` | `mb5pdlf` | Full path: `C:\dev\dev-{slug}\{slug}\` |
| Docs repo (shorthand) | `dev-{slug}\{slug}-project-library\` | `dev-mb5pdlf\mb5pdlf-project-library\` | Full path adds the `C:\dev\` root. The suffix (not prefix) form is deliberate — it sorts the docs repo next to the code repo on GitHub. |
| Drive root | `C:\dev\` | | Dropped in shorthand prose. Always spelled out in full in any literal command the agent runs — a shorthand form is not something the operating system can act on. |
| GitHub org | `sassycomapp` | | Literal, hardcoded. A fixed constant, not abstracted behind a placeholder. |

**Rule:** shorthand form is used when a step file is describing or referring to a folder
in plain language. The full absolute path is used inside any literal command. Every
occurrence of the docs-repo path in a step file includes the `dev-{slug}\` parent segment
— dropping it is an error, not an acceptable further shorthand.

---

## System Locations

| Location | Path |
|---|---|
| PDLF system home (deployed) | `C:\pdlf\` |
| PDLF dev workspace | `C:\dev\dev-makepdlf\` |
| Global library | `C:\dev\project-library-global\` |
| Project template | `C:\dev\project-template\dev-(SLUG)\` |

---

## Global/Local Folder Pairing

Every folder under `project-library-global\` has a matching local folder inside each
project's docs repo. Local holds only what's canonical to that one project.
`project-library-global` is the only source of standards and specifications — see
`[[project-library-global-registration]]`.

| Global | Local |
|---|---|
| `adr-global` | `adr-local` |
| `checklists-global` | `checklists-local` |
| `docs-standard-global` | `docs-standard-local` |
| `policy-global` | `policy-local` |
| `specifications-global` | `specifications-local` |
| `standard-operating-procedures-global` | `standard-operating-procedures-local` |
| `templates-global` | `templates-local` |

---

## GStack Paths

| Artifact | Path |
|---|---|
| Native design-doc output | `~/.gstack/projects/sassycomapp-{slug}-project-library/{user}-{branch}-design-{datetime}.md` |

Confirmed directly against the real skill source and `project-inventory.md`, not
assumed. `mb4ecom` and `mb5pdlf` are the standard; `mb-3-cs` is a known legacy exception;
`dev-makepdlf` is a non-Anvil exception (single repo, no `-project-library` segment).

---

## PDLF Artifact File Naming

| Artifact | Path | Notes |
|---|---|---|
| Step Receipt | `{docs-repo}\pdlf\step-{N}-receipt.md` | No `outputs` subfolder |
| First concept draft | `{docs-repo}\docs-local\design-doc-first-concept.md` | Permanent, written once, never overwritten |
| Working design doc | `{docs-repo}\docs-local\design-doc.md` | Current working copy |

---

## Stepwise File Naming (`dev-makepdlf\stepwise\`)

Every step's file set uses the bare `step-{N}` prefix. The skill/function name is
part of the step file's own filename only — it is never repeated into that step's
build-notes or decision-tree filenames.

| Artifact | Convention | Example |
|---|---|---|
| Step file | `step-{N}-{skill-or-function-name}.md` | `[[step-14-plan-ceo-review]]` |
| Build notes | `step-{N}-build-notes.md` | `[[step-14-build-notes]]` |
| Decision tree | `step-{N}-decision-tree.html` | `step-14-decision-tree.html` |

**Rule:** naming is governed by this file, not by matching the pattern of any other
step's existing filenames. Where an existing file's name conflicts with this table,
the existing file is wrong and gets renamed to match — this file does not get
reverse-engineered from prior naming choices.

### External Skill Source Reference

When a GStack or Matt Pocock skill's actual source (`SKILL.md`, `manifest.json`,
[[[pdlf:makepdlf-project-library/stepwise/skill-source-reference/plan-eng-review-review-sections|Plan Eng Review Review Sections]]](C:/pdlf/makepdlf-project-library/stepwise/skill-source-reference/plan-eng-review-review-sections.md), etc.) is fetched and kept as verification evidence for a step's
rebuild, it lives at `stepwise\skill-source-reference\{skill-name}-{file-name}`, not
inside `docs-local\` and not inside the step's own file. This is external, third-party
material kept for audit purposes — proof a step was verified against real source, not
assumed — and is kept distinct from PDLF's own authored files. Example:
`stepwise\skill-source-reference\plan-eng-review-manifest.json`.

---

## Migrated from `spec-architecture.md` (retired 2026-07-18)

`spec-architecture.md` was retired — it contradicted `[[deployment-procedure]]` on what
`C:\pdlf\` actually contains (a larger, pre-decision version vs. the confirmed minimal
one). Two tables from it were still accurate and are kept here pending a better permanent
home once docmap/scaffold housekeeping settles.

### Standards files relevant to stepwise skills

| Step(s) | Standard |
|---|---|
| 17, 29, 32 (Anvil IDE) | `[[spec-anvil-platform-standards]]` |
| 20 (M3 design) | `[[spec-m3-design-standards]]` |
| 35, 35A (testing) | `[[spec-testing-methodology-standards]]` |
| 22, 26 (UI) | `[[spec-ui-standards]]` |
| 27 (screen production) | `[[spec-screen-and-wireframe-production-standards]]` |
| 35, 42A (integration) | `[[spec-integration]]` |
| 35 (observability) | `[[spec-observability]]` |
| 35 (security) | `[[spec-security]]` |
| 41–45 (deployment) | `[[spec-deployment]]` |

### Reference Patterns

When a stepwise skill needs to reference content outside the stepwise package:

| Target | Pattern |
|---|---|
| Another stepwise skill | `step-{NN}-{name}.md` (same directory) |
| Shared reference doc | `[[spec-execution-discipline]]` (same directory) |
| Template | `dev-{slug}\{slug}-project-library\templates-local\...` or `templates-global\...` |
| Global spec | [[[default:specifications-global/spec-anvil-platform-standards\|Anvil Platform Mechanics]]](C:/dev/project-library-global/specifications-global/spec-anvil-platform-standards.md) |
| Global ADR | [[[default:adr-global/adr-design-rules\|Wireframe Design Rules]]](C:/dev/project-library-global/adr-global/adr-design-rules.md) |

---

*This file is adopted as of this session. Prior naming decisions scattered across build
notes and step files are consolidated here; where a step file disagrees with this file,
the step file is wrong and gets corrected to match — not the other way around.*
