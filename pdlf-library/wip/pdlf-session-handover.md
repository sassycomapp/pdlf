---
title: "pdlf-session-handover"
doc-id: "mb-5ef40e06"
updated: "2026-11-08"
---
# Session Handover — Hosting Change Batches 3 and 4

For Claude, starting a fresh session with David. Clone every repository the work needs before starting, and confirm every fact at its source before stating it.

## 1. The subject of the session

- **The decision:** every client instance (App 4) runs on the Anvil App Server, as one container on DigitalOcean App Platform, with its own database in one DigitalOcean Managed PostgreSQL cluster per business. Apps 1, 2, 3 and 5 stay on Mybizz's Anvil Business account. The price is $99 a month per client, month to month. The specification is `project-library-global\specifications-global\spec-client-instance-hosting.md`.
- **The work:** bring every live document into line with that decision, by the task list `C:\pdlf\pdlf-library\wip\hosting-change-task-list.md`.
- **The rule:** no stale or conflicting remnant of the old hosting model (one Anvil Business account per client, cloning App 3, manual schema changes per client, $150) remains in any live document.

## 2. Where the work stands

| Work | State |
|---|---|
| Batch 1, `project-library-global` | Done and committed |
| Batch 2, `pdlf` | Delivered; committed when David confirms |
| Batch 3, `mybizz-os-docs` and `project-template` | Next |
| Batch 4, `mb-3-cs-project-library` | After batch 3 |
| `{slug}-app4` repositories | Not created. Created in each business's App 3 run (Step 11, route C) as GitHub repositories only, never in Anvil; Phase G builds their content |
| PDLF Step 16 (domain modelling) | Waits for batch 4 |

## 3. Where to read

- The decision: `project-library-global\specifications-global\spec-client-instance-hosting.md`, `adr-global\adr-client-instance-architecture.md`, `adr-global\adr-dependency-update-model.md`, `specifications-global\spec-deployment.md`.
- The task list: `C:\pdlf\pdlf-library\wip\hosting-change-task-list.md`.
- PDLF: `C:\pdlf\pdlf-library\wip\pdlf-build-handover.md`, `C:\pdlf\pdlf-library\docs-local\pdlf-todo.md`.

## 4. Commit rule

- Documentation repositories (`project-library-global`, `pdlf`, project libraries, `scripts`, `mybizz-os-docs`): `cd ~ && bash /mnt/c/mybizz/scripts/commit-all.sh "message"`.
- App repositories and `project-template`: `cd <repository path> && git pull && gcp "message"`.
- Claude does not write to GitHub: Claude sends complete replacement files under their own names, with a table of each file and the folder it is saved to; David saves and commits.
