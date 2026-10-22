---
title: "README"
doc-id: "mb-2c28aeef"
updated: "2026-10-22"
---
# App Factory

The app factory holds PDLF's build: every step of the pipeline, in the phase it belongs to. When PDLF builds an application, the modules in these folders are what run. What the app factory is and why it is built this way is in [[[pdlf:pdlf-library/pdlf-explainer-docs/app-factory-explainer|PDLF — The App Factory]]](C:/pdlf/pdlf-library/pdlf-explainer-docs/app-factory-explainer.md).

## Phase folders

| Folder | Steps | What the phase does |
|---|---|---|
| `phase-a-init/` | 01–10 | 01 is the orchestrator, which runs every other module. 02–10 are the entry points for work on existing applications. |
| `phase-b-discover-and-define/` | 11–16 | Defines the application. |
| `phase-c-design-and-plan/` | 17–28 | Designs and plans the application. |
| `phase-d-scaffold-and-assemble/` | 29–34 | Builds the application's scaffold. |
| `phase-e-build-and-verify/` | 35–40b | Builds the application and verifies it. |
| `phase-f-ship-and-monitor/` | 41–46 | Releases the application and learns from the run. |
| `phase-g/` | — | The remaining applications. Created when it is designed. |

## How files are named

- Every step has the same seven files, the **set of seven**, named with the phase letter and the step number. For Step 11:
  - `b11-build-plan.md`: the step's design while it is being worked out; it is deleted once the step is built.
  - `b11-test-spec.md`: what the step must prove, and the tests it runs from the test suite in `C:\dev\project-library-global\test-suite\`.
  - `b11-config.md`: the step's fixed values (inputs, outputs, paths, skills, gate, BFT level).
  - `b11-reference.md`: what the agent does, in order.
  - `b11-explainer.md`: what the step is, how it works and why.
  - `b11-decision-tree.html`: the picture of the reference.
  - `b11-module.md`: the finished step, compiled from the config, reference, explainer, decision tree and test specification. It is written only on David's instruction (rule 2 of `C:\pdlf\AGENTS.md`).
- The older step files and build notes (such as `11-init.md` and `11-build-notes.md`) stay as source material until their step is designed.
- Step numbers are global, 01 to 46, behind the phase letter. The number is the step's identity in the ledger, the gates, the receipts and every document, so steps are never renumbered within a phase.
- Inserted steps carry a lowercase letter after the number, only to keep the files in order: `e35a`, `e38a`, `e40b`, `f42a`.
- Numbers 13, 24 and 25 are not used as steps. Each keeps one file, `b13-placeholder.md`, `c24-placeholder.md` and `c25-placeholder.md`, so the gap is visible; none has a set of seven.

## The build plan

`pdlf-build-plan.md` sits at the top of this folder. It is the blueprint for building PDLF. What has been built is recorded in `pdlf-library/docs-local/pdlf-built-report.md`, and the order the orchestrator runs the steps is in Step 1's build plan, `phase-a-init/a01-build-plan.md`. When PDLF is built, the build plan moves to `obsolete/`.
