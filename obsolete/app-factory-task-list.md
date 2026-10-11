---
title: "app-factory-task-list"
doc-id: "mb-05e1e71c"
updated: "2026-10-11"
---
# App Factory Task List

## Purpose

This list holds every task needed to replace `stepwise/` with `app-factory/`, in the order the tasks are carried out. `app-factory/` becomes the single home of PDLF's build: one folder per phase, each holding that phase's numbered files and its compiled module files. Each task is ticked off when it is done; the list is retired when every task is done.

Naming rule used throughout: lowercase kebab-case; two-digit numbers (`01`, `11`); lettered numbers in lowercase (`35a`); each file named number first, then name (`11-init.md`); each module file named `NN-module.md`.

The target layout of `app-factory/`:

- `phase-a-init`: 01 to 10 (01 is the orchestrator; 02 to 10 are the entry points)
- `phase-b-discover-and-define`: 11 to 16
- `phase-c-design-and-plan`: 17 to 28
- `phase-d-scaffold-and-assemble`: 29 to 34
- `phase-e-build-and-verify`: 35 to 40b
- `phase-f-ship-and-monitor`: 41 to 46
- `phase-g`: the remaining apps after 46, created when they are designed
- `pdlf-build-plan.md`, at the top of `app-factory/`, retired to `obsolete/` when the build is complete

---

## Section-A — Decisions to confirm before anything moves

1. The Phase A review (it covers 11 to 16) goes to `phase-b-discover-and-define`, renamed `pdlf-phase-b-review.md`, with "Phase A" corrected inside it.
2. Four module files are added for the lettered numbers: `35a-module.md`, `38a-module.md`, `40b-module.md`, `42a-module.md`.
3. The module files for the unused numbers 13 and 25: kept or removed. (Recommendation: removed.)
4. `stepwise-development-process.md`: moved to `obsolete/` or rewritten for the new layout.
5. The new wording of `AGENTS.md` rules 2 and 3 (see Section-E, task 1).

## Section-B — Finish the work already in hand

1. Place the corrected `pdlf-build-plan.md` (now with its Phase A blueprint entries and the rules every entry follows).
2. Place the corrected `pdlf-built-report.md` (now with 11 to 16 recorded as built).
3. Update `pdlf-intent.md` for the three documents settled yesterday: the run plan at `pdlf-library/docs-local/orchestrator-run-plan.md`, the build plan and the built report.
4. Commit, so that the move starts from a clean, committed state.
5. Take an inventory of `stepwise/` and `app-factory/` as they are on disk now, since files were moved by hand since the last commit, and check the list in Section-C against it.

## Section-C — Build the new layout

1. Create the six phase folders in `app-factory/`.
2. Move the module files into their phase folders, renamed `NN-module.md` (`module-01.md` becomes `phase-a-init/01-module.md`, and so on), applying the decisions in Section-A, tasks 2 and 3.
3. Move the files of 01 to 10 into `phase-a-init`, renamed: `01-orchestrator.md`, `04-undefined.md` to `10-undefined.md`.
4. Move the files of 11 to 16 into `phase-b-discover-and-define`, renamed: `11-init.md`, `11-build-notes.md`, `11-project-inventory-build-notes.md`, `11-decision-tree-v2.html`, and the same pattern for 12, 14, 15 and 16.
5. Move the files of 17 to 28 into `phase-c-design-and-plan`, renamed (`17-create-anvil-data-tables.md` and so on).
6. Move the files of 29 to 34 into `phase-d-scaffold-and-assemble`, renamed.
7. Move the files of 35 to 40b into `phase-e-build-and-verify`, renamed, with the letters lowercased (`35a-testing.md`, `38a-dependency-scan-confirm.md`, `40b-remediation.md`).
8. Move the files of 41 to 46 into `phase-f-ship-and-monitor`, renamed, lowercased (`42a-staging-integration-e2e.md`, `46-learn-junction.md`).
9. Move `pdlf-build-plan.md` to the top of `app-factory/`.
10. Move the review to its folder, per Section-A, task 1.
11. Confirm that nothing is left in `stepwise/` (`INDEX.md`, `run-plan.md`, `step-mapping.md`, `workflow.md` and `skill-source-reference/` already handled), then remove the empty folder.

## Section-D — Correct the content of the moved files

1. Repoint the short links of the form `[[step-11-init]]` inside the moved files (six files carry them) to the new names.
2. Replace every mention of `stepwise/` and of the old file names inside the moved files.
3. Correct the phase letters inside the moved files (for example, 16 says "proceed beyond Phase A", which becomes Phase B).

## Section-E — Update PDLF's own system and organisational files

1. `AGENTS.md`: the folder table (`stepwise/` removed, `app-factory/` described as the phase folders), rule 2 (removed or replaced) and rule 3 (a module file is written only by compiling its files, on the developer's instruction).
2. `README.md` at the top of `C:\pdlf`: the folder table.
3. `pdlf-intent.md`: sections 6 and 13 (where the build lives and how modules are compiled).
4. `pdlf-build-plan.md`: its preamble, its paths and its phase letters.
5. `pdlf-built-report.md`: its file paths and its phase letters.
6. `orchestrator-run-plan.md`: its phase letters and any file names it cites.
7. `pdlf-todo.md` and `config.md` in `docs-local`.
8. `stepwise-development-process.md`, per Section-A, task 4.
9. The three explainers: `pdlf-explainer.md`, `app-factory-explainer.md`, `orchestrator-agent-explainer.md`.
10. The decision records that mention the layout: `stepwise-decomposition-model`, `two-gate-extension`, `skill-use-principle`, `project-library-global-registration`, `artifact-saving-convention`.
11. The policies: `pol-testing-and-quality`, `pol-sequential-enforcement-and-deviation`, `pol-step-conditional-state`.
12. `spec-skill-design.md`, `chk-pdlf-self-test.md`, and the two Matt Pocock documents in `docs-local`.
13. `app-factory/README.md` and `pdlf-library/README.md`: noted only. They are written last, as already decided, and describe the new layout then.

## Section-F — Update the documents outside PDLF that describe it

1. `spec-nomenclature.md` in `project-library-global`: the naming rule for these files and folders.
2. Sentinel: `sentinel-config`, `sentinel-skill`, `sentinel-reference` and `sentinel-scope` in `mybizz-config-docs`, and the installed Sentinel exam skill, which reads these files by path.
3. `gstack-skills-reference` and `matt-pocock-skills-reference` in `mybizz-config-docs`.
4. `mybizz-os-explainer.md` (the app factory paragraph and the phase count).
5. The two WSL Superfile documents that cite the old layout.
6. Leave untouched: retired material and dated history records.

## Section-G — Correct what memory holds

1. Search GBrain's governed facts for statements about `stepwise/` (for example, that it is read-only) and correct each one through `mb-submit-memory`, so that agents are not told the old layout.
2. Check the global `AGENTS.md` (`~/.config/opencode/AGENTS.md`) for any mention of `stepwise/`.

## Section-H — Commit and verify

1. Commit; read the commit hook's report for any link it could not repair.
2. Rebuild the docmap.
3. Confirm that a GBrain search finds the moved files at their new paths.
4. Search all repositories once more for `stepwise` outside retired material; correct anything found.
5. Record the new layout in `pdlf-built-report.md`.
