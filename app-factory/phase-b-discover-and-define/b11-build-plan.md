---
title: "b11-build-plan"
doc-id: "mb-4f446919"
updated: "2026-10-13"
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

## Resolved — the agent never commits or pushes

Only David commits, with `commit-all`. Step 11 ends, like every step, by explaining what was done, stopping and asking David to run `/mb-close-out`.

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

---

## Later decisions

1. **No `Instructions.md` for folders created at item 12.** A standing freeze (master
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

## From `pdlf-build-plan.md`: step entry

### Phase B — Discover and Define

Ends with the gate `domain-locked` (Step 16).

#### Step 11: Init

**Must achieve:** a sound foundation for the application: its code and documentation repositories exist, are linked to GitHub and registered in GBrain, the documentation repository has the standard folder structure, and the application has its record in the ledger. Works for a new application and for an existing one.

**Starts from:** the developer's answers (new or existing; the slug; the GitHub repository addresses, and for an existing application the local paths); the project template at `C:\dev\project-template\dev-(SLUG)\`; the ledger.

**Produces:** the code repository `dev-{slug}\{slug}\` and the documentation repository `dev-{slug}\{slug}-project-library\`, both linked to GitHub; their GBrain sources, `{slug}` and `{slug}-code`; the `projects` row in the ledger; for a new application, the three pre-project files in `pre-project\`.

**Carried out by:** OpenCode.

**Must be built so that:**
- it asks first whether the application is new or existing, and runs one procedure for both, differing only in how the repositories are obtained and checked;
- the code repository always comes from Anvil, which creates it when the app is created; the agent never creates it, and asks the developer to create the app first if there is no address yet;
- the documentation repository is created on GitHub only with the developer's permission;
- for an existing application, only genuinely missing folders are created, nothing existing is changed, and broken links or registrations are corrected only with permission;
- global reference files are never copied into the project; they are referenced where they live;
- it checks the ledger is reachable with all seven tables, and that `project-library-global` is registered in GBrain;
- it ends with a self-audit that reports any error and corrects nothing without permission.

**BFT level:** Full.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md), [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md).

## From `pdlf-phase-b-review.md`: findings for this step

## Purpose

This document reviews Phase B of PDLF (Steps 11, 12, 14, 15 and 16) as a case study, before Phases C to F are built. It looks at what was done wrong, what could have been done better, how Phase B should be corrected, and how the method should change for Phase C. It judges Phase B against `pdlf-intent.md`, against the principles of mybizz-os, and against the skills catalogue. It is not a plan for Phase C.

The evidence is the five step files, their build notes and decision trees, the build plan, the built report, the old `workflow.md`, the old step mapping, and `skills-catalog.md`.

## 1. What we did wrong

**1.1 We built the steps before we had stated the intent.** The order was step file first, build notes second and intent last. Every step therefore carries assumptions that the intent later reversed: housekeeping questions at the end of every step, a ledger with six tables, a project registry and a project inventory that no longer exist, makePDLF paths and prefixes, the devlog and judgement trail, and the old rule "use a skill only when it beats OpenCode". None of these were careless; they were right when written and became wrong when the intent was settled. The cost is that all five steps now need repair before they can be packaged.

**1.2 We called the steps "built" without ever running them.** Not one of the five steps has been run against a real application. Several open questions can only be answered by a run: whether `/plan-eng-review` finds "the active plan file" inside OpenCode, where `TODOS.md` belongs, and whether the statement that "a design doc already exists" really stops GStack from re-offering `/office-hours`. mybizz-os's own principle is "present is not working, and completed is not worked". By that principle, Phase B is designed, not built.

**1.3 Each step repeats the rules that apply to every step.** Every step file spells out, in its own words, the GBrain search, the ledger row, the Step Receipt, the BFT, the two housekeeping questions and a five-action memory sequence. The same rule is written five times, slightly differently each time, so one change (such as moving close-out to `/mb-close-out`) has to be made in five places and is easily missed in one. This breaks "one fact, one home".

**1.6 Lessons went into build notes, where nobody reads them.** Each step's build notes end with "Learnings". The intent says a lesson is written into the source that the next build reads. The build notes are not that source: they are history. The lessons from Phase B ("read the skill's source first", "paste context into the skill, because it does not read our folders", "state file destinations explicitly") belong in the build plan's rules.

## 2. What we could have done better

**2.1 Too many documents per step.** Each step has a step file, build notes and a decision tree, and was also described in `workflow.md` and the step mapping. That is five places for one step, and they drifted apart. The decision trees are hand-written pictures of the step's action list, so they are a second copy of it. One step file, one build-plan entry and one built-report entry are enough.

**2.5 Skill choices were made step by step, not from the catalogue.** Each step picked the skill that came to mind. The catalogue was never read as a whole to ask: which installed skill best serves this step, and which skill is installed but unused?

## 3. How Phase B should be corrected

1. **Bring all five steps into line with the intent's rules:** close-out by `/mb-close-out`, the agent never commits, seven ledger tables, no registry or inventory, artifact copies to `C:\pdlf\output\`, no devlog or judgement trail, skills take precedence.

2. **Remove the repeated rules from the step files.** Each step file states only what is particular to it and points to the rules every step follows.

3. **Give every skill a standard context pack** at invocation: the five-app structure, the no-multi-tenancy decision, the Material 3 design standard, and the `project-library-global` standards the step applies.

9. **Run Phase B on the test application** (the Daily Intentions Tracker in `mb5pdlf`), answer the open questions from the run, and only then record the steps as finished.

10. **Move the lessons out of the build notes** into the build plan's rules, then retire the build notes and decision trees.
