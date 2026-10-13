---
title: "pdlf-handover-2026-10-13"
updated: "2026-10-13"
doc-id: "mb-50d5e2ba"
---
# PDLF Handover — 2026-10-13

## Purpose

This lets a new Claude session continue the remediation of the Phase B scope without the previous conversation. It replaces the handover of 2026-10-12. Read it fully before doing anything.

## Roles

David is the project manager acting as developer, not a programmer. He dictates by speech-to-text, so capitals and names can arrive garbled; every name is lowercase kebab-case. Claude is chief designer and chief engineer: it resolves technical questions itself and asks David only about intent. OpenCode is the worker.

## How David wants this work done (binding)

- Follow David's lead. He names the item; deal with that item only.
- Replies are two or three short paragraphs at most. No analysis, no cross-referencing for David to do, no new policies. Give a fast, solid, correct fix: kill it dead, do it once.
- Every question comes with Claude's recommended answer and the reason, in one or two sentences.
- Challenge David only where his proposal is genuinely wrong; never accept a bad proposal to please him.
- Stay strictly within the scope document's own terms. Never introduce a concept the document does not contain (in the last session, mentioning a "phase G" was rejected for this reason).
- Never send a file, artifact, command or OpenCode prompt without first asking and getting a yes. Never put a command in the same reply as an open question.
- Commands: numbered, labelled WSL terminal / OpenCode / Back to Claude, exact text to paste. Test any script on a mock before giving it.
- Only David commits (`bash /mnt/c/mybizz/scripts/commit-all.sh "message"`). Claude never commits or pushes, including in its own clones; discard local edits after delivering a file.
- `wip` folders are David's personal workspace: ignore them.

## The task

Work through Phase B of `pdlf-full-scope-v1.md` section by section, in order (B.1, B.2.1, B.2.2 … B.12), with David. At each section, settle every finding and proposal and apply the fix as fully as possible, including work in other files or folders when needed. Only what genuinely cannot be finished now is deferred.

- After each finished section, the whole scope document is reissued (only when David asks), named after the last finished section: `pdlf-full-scope-v1-b1.md`, `pdlf-full-scope-v1-b2.1.md`, and so on. Its front-matter title matches the file name.
- Deferred tasks go in `phase-b-scope-task-list-v1.md`; a new version (v2, v3 …) only when its contents change.
- David saves both to `C:\pdlf\pdlf-library\wip\`.
- The source is `C:\pdlf\pdlf-library\wip\pdlf-full-scope-v1.md`, committed in the public repository `sassycomapp/pdlf`. Clone with `git clone --depth 1 https://github.com/sassycomapp/pdlf.git`.

## Done in the last session (real, on disk, committed)

The five-app scaffold now exists for all three businesses, in Anvil, on GitHub and locally:

```
C:\dev\dev-{slug}\
  {slug}-app1               App 1, development workspace (code, Anvil app, public repo)
  {slug}-app2               App 2, master template (code, public)
  {slug}-app3               App 3, client-instance template (code, public)
  {slug}-app5               App 5, management app (code, public)
  {slug}-project-library    the one documentation repository for the business (private)
  wip                       David's personal folder
```

- Slugs keep their hyphens, all lowercase: `mb-3-cs`, `mb-4-ecom`, `mb-5-pdlf`. The rule: the slug is the business's short name as recorded at Step 11. (The build plan's "no hyphens" rule and the `mb-3-cs` → `mb3cs` rename are cancelled.)
- App names are `{slug}-app{n}`, with no descriptive word. App 4 lives on the client's own Anvil account and has no folder.
- `mb-3-cs-app1` is the former `mb-3-cs` code repository; `mb-4-ecom-*` and `mb-5-pdlf-*` replace `mb4ecom` and `mb5pdlf`.
- `commit-all.sh` and `mb-doc-check.sources` carry the new project-library names (committed).
- **No application code in GBrain.** `mb-3-cs-code`, `mb4ecom-code` and `mb5pdlf-code` were removed; agents read app code directly from the app folder. The system code sources `memory-governor-code` and `mybizz-scripts-code` stay. The project libraries are GBrain sources `mb-3-cs-project-library`, `mb-4-ecom-project-library`, `mb-5-pdlf-project-library` (federated).
- `repo-organization.md` was corrected and delivered to David to save and commit (`C:\mybizz\mybizz-os-docs\os-reference-docs\`); confirm it is committed.

## Decisions on B.1 so far

Applied (write into `pdlf-full-scope-v1-b1.md`):
1. Entry table rows, exactly as David wrote them:
   - 07 `create-client-template` | App 3 | Step 11, at the project slug question or the repository questions, depending on whether there is existing context or not.
   - 08 `create-management-app` | App 5 | the same.
   - 10 `update-management-app` | App 3 or 5 | Health check. A change to what the app does takes the feature path from Step 12; any other update goes to the step David names.
2. Entry record, item 4: the orchestrator must ask David for the feature or update statement and its short name.
3. The health check and the self-audit are standard procedures, saved in `C:\pdlf\pdlf-library\operating-procedures\`.

Awaiting David's answer (re-present briefly, with the recommendation):
4. 07: add "Steps 12 to 16 do not run for App 3", because App 3 holds only App 1's schema, one startup module and the link to App 2, so there is nothing to design. Recommended: yes. (David: "seemingly possibly yes".)
5. Entry record correction: for entries 04 to 10 the orchestrator writes the record at once to the entry-point step's ledger row; for 02 and 03 it passes the record to Step 11, which writes the business row first. Mode stays in the business row. Recommended: yes.
6. One procedure (`sop-health-check.md`) used both as Step 11's self-audit and as the health check of entries 04 to 10, or two documents. Recommended: one, because they check the same things.
7. The health check's contents, still to be designed with David. Proposed checks: ledger reachable on port 5433 with seven tables; business row matches disk; each app folder is a Git repository linked to the right GitHub repository and holds `anvil.yaml`; each app is up to date with GitHub (nothing waiting to pull from the Anvil editor); each app's `.gitignore` keeps out `.env`, credentials and test output; project library linked, with its standard folders and `pdlf-outputs` step folders; project library registered in GBrain and covered by the commit hook and `commit-all`; Matt Pocock configuration points to `CONTEXT.md` and `adr-local`. A failure is reported, nothing is fixed without permission, and work does not start until all pass.

## Effect on the rest of the scope document

The scope document was written before today's decisions. While remediating each section, correct it to:
- folder and repository names `{slug}-app1`, `-app2`, `-app3`, `-app5`, `{slug}-project-library` (it still says `{slug}-app-1` and the like);
- slugs with hyphens; no mention of the `mb3cs` rename;
- B.2.2 and B.10 decision 1: settled. No application code in GBrain.

## Deferred tasks (to become `phase-b-scope-task-list-v1.md` when David asks)

1. Add the rule "no application code as GBrain sources" to the PDLF build plan and the relevant explainers.
2. Correct the build plan's project scaffold (section 1) to the names above, and remove its "no hyphens" rule and the `mb3cs` rename line.
3. Replace the old names everywhere they still appear: `mb4ecom`, `mb5pdlf`, the old App 1 path `...\dev-mb-3-cs\mb-3-cs\`, the removed `-code` sources and `{slug}-app-1` forms. Known places: the `pdlf`, `mybizz-os-docs`, `mybizz-config-docs` and `project-library-global` repositories; `~/.config/opencode/AGENTS.md` and the skills under `~/.config/opencode/skills/` (`mb-close-out`, `mb-project-docs`, `mb-config-gbrain`, `mb-config-graphify`, `mb-config-opencode`, `mb-config-anvil-agent-references`); `/mnt/c/mybizz/scripts/install-project-docs.py`; each project folder's `README.md`, and `mb4ecom-config.yaml` and `mb5pdlf-config.yaml` (rename them too). One tested scripted replacement per repository.
4. Graphify's settings still point at the old App 1 path. Fix them, or remove Graphify (David doubts its benefit).
5. Check whether the memory governor's project list knows `mb4ecom` or `mb5pdlf`. If so, re-register them under the new names, because a mismatch with GBrain source names makes governed facts fail to arrive.
6. Removing `mb-3-cs-code` deleted 2 facts stored in it. Check the memory governor's register and restore them if they were governed.

## Context still valid from the 2026-10-12 handover

- PDLF lives at `C:\pdlf` (WSL `/mnt/c/pdlf`); `app-factory/pdlf-build-plan.md` is its single forward-looking document; every step has its set of six files in its phase folder.
- Claude's own clones: `git clone --depth 1 https://github.com/sassycomapp/<repo>.git`. Public: `pdlf`, `mybizz-os-docs`, `mybizz-config-docs`, `project-library-global`, and all twelve app repositories. Private: the three project libraries.
- Never write a file in Python with `open(p,'w').write(open(p).read()...)`: it empties the file first.
- Later, separate jobs: the GBrain upgrade (0.59 to 0.60); stale GBrain entries `desktop/pdlf-discovery` and `desktop/pdlf-intent-map`; the Cupcake gate proof; the testing component.

## Next action

Re-present B.1 items 4 to 7 above, one at a time and briefly, then continue with B.2.1.
