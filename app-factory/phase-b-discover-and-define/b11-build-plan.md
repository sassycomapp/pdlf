---
title: "b11-build-plan"
doc-id: "mb-4f446919"
updated: "2026-10-12"
---

## From `11-build-notes.md`

# Step 11 — Build Notes

**Purpose:** A running record of the decisions, corrections, and reasoning made while
building `[[11-init]]` itself. This is not a runtime artifact — Step 11 does not
generate this file when it runs against a real project. It is our own build history, kept
so that if something about this step later seems strange, we can see why it is the way it
is.

**Status of this file:** This replaces the earlier `step-11-output.md`, which was
misnamed and contained the wrong content (a runtime summary, not a build history — and it
used a receipt path we've since corrected). This file takes over its slot with a
different purpose.

**Where this lives:** Stays in `dev-makepdlf` as project build history. It is not one of the
runtime reference files a step points to, so it does not ship as part of the PDLF package
that goes to `C:\pdlf`.

---

## Decisions made

1. **Step 11 does branch by entry mode — corrected.** An earlier version of this file
   claimed the opposite ("does not branch," hands existing-project work to
   `step-02-existing-registration.md`). That was true of an early draft, but is no longer
   accurate. `[[11-init]]` now branches internally at item 4 (new vs. existing), and
   `step-02-existing-registration.md` is retired — its folder-completion, ledger, and
   remote-confirmation jobs were absorbed directly into Step 11's existing-project branch
   (items 11–15).

2. **Receipt path corrected.** The step receipt is saved at
   `dev-{slug}\{slug}-project-library\pdlf\step-{N}-receipt.md`. There is no `outputs`
   subfolder. Two older documents ([[[pdlf:obsolete/docmap|Docmap]]](C:/pdlf/obsolete/docmap.md), and the original `step-11-output.md`)
   showed an `outputs` subfolder — both were wrong and are superseded by this decision.

3. **BFT level confirmed as Full.** Step 11 creates the project's structural foundation —
   ledger row, registry entry, folder tree — which is decision-heavy enough to warrant
   the full six-question BFT, not Light or None.

4. **Global reference files are never copied into a project.** A new project references
   global specs, policies, and templates where they already live. Nothing gets copied in
   at init.

5. **Full paths, not shorthand.** When referring to folders or files across documents, we
   spell out the complete path rather than using ambiguous shorthand — this avoids
   confusion between, for example, `docs-local` inside `dev-makepdlf` versus `docs-local`
   inside a project like MB5PDLF, which are two different folders with the same name.

---

## Resolved — path format inside step files

This convention applies across all step files, not just Step 11.

- Docs repo folder → `dev-{slug}\{slug}-project-library\` — the docs repo carries the
  slug prefix deliberately, so it sorts next to the code repo on GitHub.
- Code repo folder → `{slug}` (shorthand for `dev-{slug}\{slug}\`, understood by
  convention — Anvil, git, and this whole working environment identify the app by the
  slug alone)

This is the form used when a step file is describing or referring to a folder in plain
language. It is not the form used inside an actual command the agent will run. Any literal
command that touches disk (git, cd, file operations) still needs the real, complete,
absolute path starting with `C:\dev\` — a shorthand form is not something the operating
system can act on.

## Resolved — self-audit step requires permission, not silent correction

The decision tree's "self-audit, correct any errors immediately" step surfaces problems
immediately, but does not fix anything without asking first. Confirmed directly, and
consistent with the global AGENTS.md's default-to-ask and no-rubber-stamping rules.

## Resolved — no automatic git operations, ever

There is never an automatic, unasked commit or push, at any stage, for any reason. The
early setup check (items 18–19) is an early *ask*, not an automatic action — the agent
requests permission right after GBrain registration, rather than waiting until
end-of-step housekeeping. This preserves the original intent (catching a broken setup
immediately) without violating the global AGENTS.md rule that git operations are always
permission-only.

## Resolved — new-project entry never invents a code repo

The code repo always originates in Anvil — Anvil creates it automatically when the app is
created there. If the developer doesn't yet have a URL, Step 11 instructs them to set up
the app in Anvil first, then asks again. The agent never creates the code repo itself.
The docs repo is different: the agent creates it, but only after asking the developer's
permission first (item 9).

## Resolved — the disposition-audit model is retired entirely

`step-02-existing-registration.md`, `step-03-resume-point-audit.md`, and
the retired `sop-existing-project-resume-audit.md` are all gone. The model they implemented — assign
SKIP / RE-RUN / RUN-AS-NEW to steps 12–34 based on whether existing work looks valid —
was replaced by a different principle: submitting an existing project to PDLF means
redeveloping it around its canonical concept, not auditing or maintaining what already
exists. Every step always runs, for every project. What differs for an existing project
is only the material a step starts from, never whether it runs. This is why Step 11's
existing-project branch (items 11–15) verifies and corrects what's already there rather
than deciding whether to skip anything downstream.

## Resolved — Step 11 registers project-library-global with GBrain

Closes an open item from Step 14/15/16's build: their local/global conflict check depends
on `project-library-global` being a registered, queryable GBrain source, but no step was
confirmed responsible for making that registration happen. Resolved: Step 11 does it
(item 17a), every invocation, both entry modes — same treatment as the per-project
`{slug}` and `{slug}-code` sources at item 17, just checked-and-registered-if-missing
rather than always-fresh, since it's shared infrastructure that only needs registering
once but must never be silently assumed present.

## Resolved — global AGENTS.md location

The global AGENTS.md referenced throughout this file (permission rules, default-to-ask,
git operations being permission-only, no batching without permission) lives at:

```
\\wsl.localhost\Ubuntu\home\dev-p\.config\opencode\AGENTS.md
```

This is the Windows-side UNC path to reach it from outside WSL; from inside WSL it's the
ordinary `~/.config/opencode/AGENTS.md`. This governs every OpenCode session, not just
Step 11 — it's the source every "per the global AGENTS.md" reference in this step (and
across all the step files) actually points to. The fact was originally recorded
in `obsolete/todo-stepwise-development).md` item 8 and had not been carried into this file
until the housekeeping pass surfaced it as a fact present nowhere else in the active
document set — recovered here rather than lost when that todo file is retired.

## Resolved — project-inventory.md integration

`C:\dev\dev-root\project-inventory.md` is the authoritative reference for path/credential
correctness across all projects.
`dev-makepdlf` and `C:\pdlf` are both excluded — neither is a project Step 11 onboards. Full
detail in [[[pdlf:app-factory/phase-b-discover-and-define/b11-build-plan|Step 11: Project Inventory Build Notes]]](C:/pdlf/app-factory/phase-b-discover-and-define/b11-build-plan.md).

---

## Discoveries about the project template

- The template lives at `C:\dev\project-template\` and has a `dev-(SLUG)` folder
  containing both a code-repo side and a `project-library` side.
- Every folder inside the template has its own short `Instructions.md` explaining what
  belongs there. These are currently one-line placeholders and are earmarked as a
  follow-on task once 11-init is finished (see the main todo file).
- The three pre-project files (`[[01-project-brief]]`, `[[02-scoping-ideas]]`,
  `[[03-constraints-and-notes]]`) are not pre-filled by the template. The agent asks the
  developer to supply them, and the developer places them in that exact folder with
  content unique to the project being built.

---

## Idiosyncrasies worth remembering

- `step-11-output.md` arrived from an earlier draft pass with no clear origin or purpose,
  and initially looked like dead weight. It was repurposed into this file instead of
  being deleted outright, once its intended use (a build log for us, not a runtime
  artifact) became clear.

---

## Drafting decisions, first draft (confirmed)

1. **AGENTS.md source.** When a project is missing AGENTS.md, it is created from the
   global template at `C:\dev\project-library-global\docs-standard-global\AGENTS.md` —
   not the per-project scaffold template, since existing-project entry never fetches that
   template at all. Confirmed.

2. **Git commit and push is asked, not automatic.** Only `git init` (creating the empty
   repo) runs automatically. The actual commit and push only happen when the developer
   answers yes to the housekeeping question — matching the policy that commit/push is
   never auto-run. Confirmed.

3. **GStack `/sync-gbrain` is kept, not replaced with raw commands.** Initially removed
   on skill-use-principle grounds (a plain `gbrain sync`/`gbrain embed` command seemed to
   do the same job without a skill wrapper). Reversed on developer's direct experience:
   the GStack skill has proven more thorough and reliable than raw commands, which have
   struggled in practice. The housekeeping question now invokes `/sync-gbrain` against
   both the doc source and code source.

   **Superseded — see entry 4 below.** This decision no longer holds. `/sync-gbrain` is
   removed from Step 11 entirely, replaced by the memory-governor sequence.

---

## Later decisions

1. **`/sync-gbrain` replaced with the `mb-submit-memory` skill, submitting through the
   memory governor.** The old `/sync-gbrain` command reads whatever files happen to be
   sitting in a registered folder, with nothing checking them first — which means it
   could silently undo a decision the memory governor had already made about a piece of
   content. This is a system-wide change (master task list, item 9.2), applied here to
   Step 11's two `/sync-gbrain` mentions: item 19 (the early check) and item 22
   (end-of-step housekeeping). Item 19 now invokes the `mb-submit-memory` skill against
   any real, developer-written content. Item 22's second housekeeping question is now a
   five-step sequence rather than a single command: commit and push to GitHub; invoke
   `mb-submit-memory` for each real file; run `gbrain dream` for real (a dry run writes
   nothing and cannot serve as a check); run `gbrain eval suspected-contradictions`
   immediately afterward; review what it reports, with real attention to anything
   marked high-severity. Only real, developer-written content goes through
   `mb-submit-memory` — the templated boilerplate Step 11 copies at item 7 (`AGENTS.md`,
   `README.md`, `CLAUDE.md`, `opencode.json`) carries nothing genuinely new to check and
   is never submitted. Confirmed with the developer this also covers the existing-project
   case, where many pre-existing files might need submitting at once — no special
   handling needed, since `mb-submit-memory` already enumerates a folder's real files and
   submits each individually, one at a time, per its own governing skill file.

   **Skill built and installed, 2026-08-25.** The `mb-submit-memory` skill itself did not
   exist when the decision above was first made — item 19 and item 22 originally said
   only "hand content to the memory governor," a real gap with no concrete mechanism
   behind it. Rather than leave that as a standing gap to revisit later, the skill was
   written in full and installed before this file was finalized: it queries GBrain for
   related content, forms a real confidence score and contradiction judgment using a
   concrete, bounded method (not left to improvisation), reports its findings, and only
   submits to the memory governor's real API after explicit developer approval. See the
   skill's own file for the full procedure.

2. **No `Instructions.md` for folders created at item 12.** A standing freeze (master
   task list, item 2.2) is currently in effect on creating any further `Instructions.md`
   files anywhere, until a decided format lands. Item 12 (existing-project entry) can
   create genuinely missing folders — the one case in this step where a folder is
   created fresh rather than copied in from the template. Decided with the developer:
   any folder created here does not get an `Instructions.md`, for now, until the freeze
   lifts.

## From `11-project-inventory-build-notes.md`

# Step 11 — project-inventory.md Integration — Build Notes

**Status: fulfilled.** Kept
here as the record of why, not as a pending task.

**Destination:** `[[11-init]]`. Added alongside the existing registry-write action
(`C:\pdlf\registry\projects.json`) — this is functionally a second registry, focused on
path/credential verification rather than PDLF run state.

## The rule

`project-inventory.md` lives at `C:\dev\dev-root\project-inventory.md` — authoritative reference
for path/credential correctness across all projects.

Every Step 11 run, for either entry mode, does this against it:

1. Check whether the current project already has an entry.
2. **No entry** — add one, once Step 11 has established the real local paths, GitHub
   URLs, GBrain source names, and GStack path for this project. Applies to a genuinely
   new project and to a legacy project getting its first-ever entry.
3. **Entry exists** — verify it against what's actually there right now (local paths,
   GitHub URLs, GBrain sources, GStack path). Any mismatch is surfaced to the developer
   directly — never silently accepted, never silently overwritten.

## Exceptions — confirmed

- `dev-makepdlf` — has a manually-added entry, made before PDLF existed to run Step 11
  against anything. Left alone. Not something Step 11 ever touches.
- `C:\pdlf` — never gets an entry. It's the deployed tool, not a project PDLF builds.

## Dependency — corrected

The GBrain source-scoping rule now lives in [[[pdlf:pdlf-library/policy-local/pol-memory-and-knowledge|Policy: Memory and Knowledge]]](C:/pdlf/pdlf-library/policy-local/pol-memory-and-knowledge.md) (the earlier
reference to a "the retired `spec-execution-discipline-build-notes.md`" was to a file that was
mis-categorized and later retired — the rule was properly relocated into that policy,
not left as a standalone note). That policy can now use this file's `project-inventory.md`
integration as the authoritative lookup for exact GBrain source names.
