---
title: "pdlf-handover-2026-10-12"
updated: "2026-10-12"
doc-id: "mb-06cef0da"
---
# PDLF Handover — 2026-10-12

## Purpose

This document lets a new Claude session continue PDLF work without the previous conversation. Read it fully before doing anything. It replaces the handover of 2026-10-11.

## Roles

David is the project manager acting as developer, not a programmer. He dictates by speech-to-text, so names can arrive garbled; all his document names are lowercase kebab-case. Claude (web interface) is the architect and engineer: it resolves technical questions itself and asks David only about intent. OpenCode and its models are the worker.

David's stored preferences apply in full. The ones that mattered most in the last session:
- Short, plain replies; findings, warnings and steps kept in separate labelled parts.
- Discuss first. Ask clarifying questions instead of assuming. No files, commands or packages until David says the discussion is finished. Never put a command in the same reply as an open question.
- One item at a time, in the order David chooses.
- When David asks for substance, give real substance: what a step does, how, with which skill, why. A label such as "valuable" or "drafted" is not information.
- Never dismiss old drafts. The old scoping in the step files holds real, hard-won design work.
- Numbered steps labelled WSL terminal / Windows / Back to Claude, with the exact command to paste.

## The system, as it stands now

- PDLF lives at `C:\pdlf` (WSL `/mnt/c/pdlf`), repository `sassycomapp/pdlf`. It is currently public, on purpose, so Claude can read it.
- **`app-factory/pdlf-build-plan.md`** is the single forward-looking document for PDLF as a whole. The former intent document was merged into it and retired to `obsolete/`. Its preamble covers: what PDLF is and the team; what a project is (one business, at `C:\dev\dev-{slug}\`, with code repositories `{slug}-app-1`, `-app-2`, `-app-3`, `-app-5`, one `{slug}-project-library`, and `wip`); control and gates; the five-app structure (App 2 is always a clone of App 1; App 4 is a clone of App 3 on the client's own Anvil account, owned by David and named for the client's business; hosting at `1.mb3cs.site` and so on); the entry points; how PDLF runs; knowledge, skills, learning and records; the document life cycle; the rules every step follows; what is still to be settled; and section 10, how each step is designed.
- **Entry points (Steps 2 to 10)**: `/pdlf-init` starts Step 1, the orchestrator, which offers exactly one of: 02 new-app-no-context and 03 new-app-with-context (both enter Step 11); 04 add-feature-main-app and 05 update-main-app (App 1); 06 compile-master-template (App 2); 07 create-client-template (App 3); 08 create-management-app (App 5); 09 add-feature-management-app and 10 update-management-app (App 3 or App 5). Existing-app entry points first run a health check. Features take the feature path from Step 12; updates that change what the app does are features, other updates go to the step David names.
- **The app factory** is flat by phase (`phase-a-init` to `phase-f-ship-and-monitor`). Every step has its **set of six**: `{letter}{number}-build-plan.md`, `-config.md`, `-reference.md`, `-explainer.md`, `-decision-tree.html`, `-module.md` (for example `b11-...`). Steps 13 and 25 have only `b13-placeholder.md` and `c25-placeholder.md`. Lettered steps keep their letters (`e35a`, `e38a`, `e40b`, `f42a`).
- **All step-specific material is now inside the step files.** The old numbered step files went into each step's reference; build notes, the old build-plan entries, the Phase B review findings, the step mapping rows, BFT levels, gates, the run plan (into `a01-build-plan.md`), the orchestrator explainer (into `a01-explainer.md`), and step-specific passages from policies, specifications and the to-do list went into each step's build plan or config. Every moved block starts with a heading `## From \`source-file\`: ...`. Nothing is arranged yet; it is all in the right step.
- **Step outputs** go to each project library's `pdlf-outputs\{step}\` folder (created for mb-3-cs, mb4ecom, mb5pdlf, 50 folders each). Nothing an application produces is kept in `C:\pdlf`; the old `output/` folder is gone.
- `stepwise/` is gone. The old Phase B review and step mapping are in `obsolete/`.

## The next task: Full Scope

David will provide the overview document **V4** (`pdlf-overview-v4.md`, in `C:\pdlf\pdlf-library\wip\`). In the new session it is renamed **Full Scope**, and the work is versioned:

- **Full Scope V1**: build out Phase B (Steps 11 to 16) in full depth. Leave everything else in the document as it is, including the statement that Phase A is not yet designed.
- **V2**: Phase C. **V3**: Phase D. **V4**: Phase E. **V5**: Phase F. Then Phase A.

Versioning rule: produce a new version only when David asks, or when both agree a point worth a version has been reached. Never drift into many small versions.

**What "build out" means.** Take a deep dive into every file of every step in that phase and extract every piece of relevant information: every action in order, every branch and decision point, every rule and the reason behind it, every skill and how it is invoked, inputs, outputs, gates, thinking-check levels, failure handling, and every open point. Then expand on it to scope for excellence: where the existing design is thin, propose what it should be, clearly marked as a proposal. The aim is a deep scope of PDLF, not a summary.

**For Phase B, read all of these in full** (in `app-factory/phase-b-discover-and-define/`):
- `b11-`, `b12-`, `b14-`, `b15-`, `b16-` `build-plan.md` (step entry, full build notes, Phase B review findings, moved policy passages)
- the same steps' `reference.md` (the full old step files: action lists, branches, rules)
- the same steps' `config.md` (type, handler, gate, BFT level and reason)
- `b11-` to `b16-decision-tree.html` (branch logic)
- the 923-line copy of the `/plan-eng-review` skill source, now inside `b15-build-plan.md`
- for context: `a01-build-plan.md` (the run plan), the system build plan, and `pdlf-library` specifications (`spec-execution-discipline`, `spec-gate-procedure`, `spec-artifact-handover`, `spec-bft`)

End each version with the list of files read, so David can see nothing was skipped.

**Known gaps David wants in the scope** (raise them where they belong, as proposals): Sentinel review throughout the pipeline; `secure-software-engineering` throughout; Anvil's own skills (`anvil-agent-references`, `data-models` and others) throughout; the no-shared-database rule given to every skill; Step 11 reshaped for all entry points, not only new apps; Apps 2 to 5 (clone release, client template, first client and provisioning, management app); learning through the memory governor and `mb-submit-memory` at Step 46.

## How work is done

- Claude keeps its own clones in its workspace: `git clone --depth 1 https://github.com/sassycomapp/<repo>.git`. To refresh: `git fetch --depth 1 origin && git reset --hard FETCH_HEAD`. Public: `pdlf`, `mybizz-os-docs`, `mybizz-config-docs`, `project-library-global`. Private: `mb-3-cs-project-library` and the other project libraries.
- Changes are delivered as a zip holding a patch and an `apply.sh`, which checks the patch (`git apply --check --index`) before applying, and runs `git update-index -q --refresh` first. David saves the zip to `C:\temp\`. If a download is awkward, a single pasteable command is better.
- Test every patch against a fresh clone before sending.
- Only David commits: `bash /mnt/c/mybizz/scripts/commit-all.sh "message"`. Prefix `MB_DELETE_OK=1` when a change removes documents while adding others. The commit hook assigns doc-ids (new files may carry their own `doc-id: "mb-xxxxxxxx"`; check uniqueness), repairs links on moves, and turns links to deleted documents into plain words.
- When a merge or removal touches documents linked from other repositories, repoint those links in the same package.

## Warnings from the last session

- **Never write a file in Python with `open(p,'w').write(open(p).read()...)`**: it empties the file before reading it. That mistake emptied `C:\pdlf\.gitignore`, and `.env` (the ledger passwords) was committed to the public repository. It was fixed: `.gitignore` restored, `.env` untracked, and both ledger passwords changed (in the database, `C:\pdlf\.env` and Windows `pgpass.conf`). The old passwords remain in GitHub history but no longer work. Backups holding the old passwords are in `~/backups` on David's machine; David can delete them.
- Do not offer packages or commands before the discussion is finished.

## State at handover

- Everything up to the Step 15 absorption and the relinking is committed and pushed.
- Not yet committed: the `C:\pdlf\pdlf-library\wip\` folder with overview V2 and V4 (David saves and commits these himself).

## Open items, in order

1. Full Scope V1 (Phase B), then V2 to V5 and Phase A, as above.
2. Later, separate jobs: rename `mb-3-cs` to `mb3cs` everywhere (starts in Anvil); the GBrain upgrade (0.59 to 0.60); stale GBrain entries `desktop/pdlf-discovery` and `desktop/pdlf-intent-map`.
3. The Cupcake gate proof and the testing component: set aside; each starts fresh when reached.
