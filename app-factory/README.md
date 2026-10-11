---
title: "README"
doc-id: "mb-ab3dbf19"
updated: "2026-10-11"
---
# App Factory

The app factory holds PDLF's build: every step of the pipeline, in the phase it belongs to. When PDLF builds an application, the modules in these folders are what run. What the app factory is and why it is built this way is in [[[pdlf:pdlf-library/pdlf-explainer-docs/app-factory-explainer|PDLF — The App Factory]]](C:/pdlf/pdlf-library/pdlf-explainer-docs/app-factory-explainer.md).

## Phase folders

| Folder | Steps | What the phase does |
|---|---|---|
| `phase-a-init/` | 01–10 | 01 is the orchestrator, which runs every other module. 02–10 are the entry points for work on existing applications. |
| `phase-b-discover-and-define/` | 11–16 | Defines the application. Also holds `pdlf-phase-b-review.md`. |
| `phase-c-design-and-plan/` | 17–28 | Designs and plans the application. |
| `phase-d-scaffold-and-assemble/` | 29–34 | Builds the application's scaffold. |
| `phase-e-build-and-verify/` | 35–40b | Builds the application and verifies it. |
| `phase-f-ship-and-monitor/` | 41–46 | Releases the application and learns from the run. |
| `phase-g/` | — | The remaining applications. Created when it is designed. |

## How files are named

- Every file starts with its step number: `16-domain-modeling.md`, `16-build-notes.md`, `16-decision-tree.html`.
- Each step has one module file beside its step files, `NN-module.md`. The module is the step compiled into a single unit. It stays a placeholder until David instructs the compile (rule 2 of `C:\pdlf\AGENTS.md`).
- Step numbers are global, 01 to 46. The number is the step's identity in the ledger, the gates, the receipts and every document, so steps are never renumbered within a phase.
- Inserted steps carry a lowercase letter: 35a, 38a, 40b, 42a.
- Numbers 13 and 25 are not used as steps. Their module files are kept.

## The build plan

`pdlf-build-plan.md` sits at the top of this folder. It is the blueprint for building PDLF. What has been built is recorded in `pdlf-library/docs-local/pdlf-built-report.md`, and the order the orchestrator runs the steps is in `pdlf-library/docs-local/orchestrator-run-plan.md`. When PDLF is built, the build plan moves to `obsolete/`.
