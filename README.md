---
title: "README"
doc-id: "mb-eba493f3"
updated: "2026-10-12"
---
# PDLF

PDLF (Project Development Lifecycle Framework) is an implemented system, not a project. It builds Anvil applications. The developer chooses an application and starts PDLF's orchestrator in OpenCode; the orchestrator then runs the modules in order, one per pipeline step, from the application's definition to its release. The applications PDLF builds are the projects. PDLF itself has no code repository.

PDLF draws its knowledge and standards, Anvil knowledge included, from `project-library-global`, a separate and permanent repository. This repository holds only how PDLF itself works.

## Connections

| Item | Value |
|---|---|
| GitHub | `sassycomapp/pdlf` (private), branch `main` |
| GBrain | source `pdlf` (federated), covering all of `C:\pdlf` |
| Local path | `C:\pdlf` (WSL `/mnt/c/pdlf`) |

## Folders

| Folder | What it holds |
|---|---|
| `app-factory/` | The build, one folder per phase (`phase-a-init` to `phase-f-ship-and-monitor`). Each phase folder holds the set of six for every step (for example `b11-build-plan.md`, `b11-config.md`, `b11-reference.md`, `b11-explainer.md`, `b11-decision-tree.html` and `b11-module.md`). The module is the step compiled into a single unit; until then it is empty. The older step files and build notes stay beside them as source material. `pdlf-build-plan.md` sits at the top. See `app-factory/README.md`. |
| `pdlf-library/` | The shared machinery every module relies on: ADRs, specifications, policies, templates, explainers and supporting documents. See `pdlf-library/README.md`. |
| `output/` | Temporary copies of the artifacts produced while one project runs through PDLF, kept by producing tool in `output-gstack/`, `output-opencode/` and `output-pocock/`. Each artifact is copied into the project's own folders, then cleared from here. Not version-controlled. |
| `desktop/` | The developer's working documents for the current work. |
| `obsolete/` | Retired files. |

## Files at the top

| File | Purpose |
|---|---|
| `AGENTS.md` | Standing rules for any agent working here. Read it before starting. |
| `.env` | Connection settings and passwords for the PDLF ledger. Never committed. |
| `.gitignore` | Keeps `output/`, `.env` and compiled Python files out of Git. |
| `.gbrain-source` | Names this repository's GBrain source (`pdlf`). |
