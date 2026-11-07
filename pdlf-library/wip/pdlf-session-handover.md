---
title: "pdlf-session-handover"
doc-id: "mb-5ef40e06"
updated: "2026-11-07"
---
# Session Handover — The Platform Question

For Claude, starting a fresh session with David. Clone every repository the work needs before starting, and confirm every fact at its source before stating it.

## 1. The subject of the session

- **The problem:** Anvil's Business plan costs $99 a month per client instance. With that cost, the price to a client rises to $150–$200 a month, which the market does not pay. Anvil's constraints also inhibit the applications, even on the Business plan.
- **David's work so far:** David has found alternative solutions. They may change the five-app structure slightly, or not at all.
- **The impact:** the new solutions will definitely impact PDLF.
- **The purpose of the session:** David presents the alternatives; the session works through them with him and settles what they mean for the platform, the five-app structure and PDLF.
- The session is a scoping discussion: no files, prompts or commands until David agrees the design is ready.

## 2. Where the work stands

| Work | State |
|---|---|
| PDLF Step 15 (`/plan-eng-review`) on `mb-3-cs` App 1 | Closed. Outputs, corrections and close-out committed; the memory review queue is empty |
| App 1 theme | Switched to `m3-custom-theme` (package `m3`, master branch of the Anvil app `7USO6DVZSIIWA5QX`); theme files match the theme; colours Professional Blue Light; Include Bootstrap 3 and Legacy class names off |
| App 1 old forms | 91 YAML forms still name the removed theme by `dep_dapp798jbsn8mq` and draw nothing in the designer. Each is replaced, feature by feature, by `mb-form-builder` |
| Phase C UI tools (batch 5) | Not started. Recorded in `pdlf-todo.md` item A1a; done before Step 17 is rebuilt |
| PDLF Step 16 (domain modelling) | Not started. Held until the platform question is settled, because a platform change can alter where and how the business's data lives |

## 3. Where to read

- The five-app structure: `project-library-global\specifications-global\spec-five-app-architecture-model.md`; `project-library-global\adr-global\adr-client-instance-architecture.md`, `adr-dependency-based-not-multi-tenant.md`, `adr-client-instance-readme-five-app-system.md`, `adr-common-architecture-across-mybizz-applications.md`.
- Deployment: `project-library-global\specifications-global\spec-deployment.md`.
- The application: `mb-3-cs-project-library\docs-local\mb-3-cs-concept.md`, `mb-3-cs-architecture-explainer.md`, `mb-3-cs-architecture-reference.md`; the design doc `mb-3-cs-project-library\docs-local\design\app1\design-doc.md`.
- PDLF: `C:\pdlf\pdlf-library\wip\pdlf-build-handover.md`, `C:\pdlf\pdlf-library\docs-local\pdlf-todo.md`.
- The Phase C UI plan: `C:\pdlf\pdlf-library\wip\pdlf-phase-c-ui-workflow.md`.

## 4. Commit rule

- Documentation repositories (`project-library-global`, `pdlf`, project libraries, `scripts`, `mybizz-os-docs`): `cd ~ && bash /mnt/c/mybizz/scripts/commit-all.sh "message"`.
- App repositories and `project-template`: `cd <repository path> && git pull && gcp "message"`.
- Claude does not write to GitHub: Claude sends complete replacement files under their own names, with a table of each file and the folder it is saved to; David saves and commits.
