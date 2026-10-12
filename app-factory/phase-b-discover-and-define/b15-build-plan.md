---
title: "b15-build-plan"
doc-id: "mb-9f7cd52b"
updated: "2026-10-12"
---

## From `15-build-notes.md`

# Step 15 (plan-eng-review) — Build Notes

Captured during discussion, before this step file was rebuilt. Points to carry forward.

## Task list (matches [[[pdlf:app-factory/phase-b-discover-and-define/b15-reference|15-plan-eng-review]]](C:/pdlf/app-factory/phase-b-discover-and-define/b15-reference.md))

1. Query GBrain (automatic, read-only) — sources explicitly nominated
2. Check Step 14's mode/ledger row to determine which plan artifact exists
3. Assemble context: plan artifact, design doc, first-concept draft, [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md) output
4. Local/global conflict check — same OpenCode-run mechanics as Step 14
5. Invoke [[[pdlf:app-factory/phase-b-discover-and-define/b15-reference|/plan-eng-review]]](C:/pdlf/app-factory/phase-b-discover-and-define/b15-reference.md), pasting everything, stating a design doc already exists
6–12. Skill runs: pre-review audit → Step 0 (Scope Challenge) → 4-section review →
   Test Plan Artifact write → Required Outputs → Outside Voice → GSTACK REVIEW REPORT
13–15. Capture and copy both artifacts; verify
16–22. Ledger row, Step Receipt, BFT Full, housekeeping, present, continue

## Correction — the five-document TDD cluster was never real

Every prior draft of this step (including the one carried into
`docs-local/todo-makepdlf.md` §3.2, marked `[COMPLETE 2026-07-10]`) assumed
[[[pdlf:app-factory/phase-b-discover-and-define/b15-reference|/plan-eng-review]]](C:/pdlf/app-factory/phase-b-discover-and-define/b15-reference.md) produces five separate documents: [[[mb-3-cs-project-library:docs-local/architecture|architecture]]](C:/dev/dev-mb-3-cs/mb-3-cs-project-library/docs-local/architecture.md) (mb-3-cs project library),
[[[mb-3-cs-project-library:docs-standard-local/integration-architecture|integration-architecture]]](C:/dev/dev-mb-3-cs/mb-3-cs-project-library/docs-standard-local/integration-architecture.md) (mb-3-cs project library), the retired `security-architecture-canonical.md`,
[[[mb-3-cs-project-library:docs-standard-local/globals-contract|globals-contract]]](C:/dev/dev-mb-3-cs/mb-3-cs-project-library/docs-standard-local/globals-contract.md) (mb-3-cs project library), [[[mb-3-cs-project-library:docs-local/authoritative-schema|authoritative-schema]]](C:/dev/dev-mb-3-cs/mb-3-cs-project-library/docs-local/authoritative-schema.md) (mb-3-cs project library). Read Plan Eng Review Review Sections
directly (925 lines, full source, not excerpts) — none of these filenames
appear anywhere in the skill. Searched every `.md` reference in the file;
only two exist: `TODOS.md` (referenced, not created by this skill) and the
Test Plan Artifact (the one real, separate file this skill produces, exact
path confirmed).

This is the same class of error as the bare-`{slug}` path caught during
Step 14's build — an assumption that was never checked against source and
got carried forward, marked complete, and cited by later documents (in this
case, the retired `todo-makepdlf.md`) as settled fact. Logged as
`obsolete/todo-stepwise-development).md` item 8 for correction once this step
ships.

## What Step 15 actually produces, confirmed against source

- **One separate file:** the Test Plan Artifact, exact path
  `~/.gstack/projects/{slug}/{user}-{branch}-eng-review-test-plan-{datetime}.md`.
  Fixed structure (Affected Pages/Routes, Key Interactions, Edge Cases,
  Critical Paths). Consumed automatically by [[[pdlf:app-factory/phase-e-build-and-verify/e38-reference|/qa]]](C:/pdlf/app-factory/phase-e-build-and-verify/e38-reference.md) and `/qa-only` — confirmed
  in source, not just claimed.
- **Everything else lands inside the plan file** — the same plan file Step
  14 was operating on, not a new one: the 4 sections' resolved findings, the
  Required Outputs subsections (NOT in scope, What already exists, TODOS.md
  updates, Diagrams, Failure modes, Worktree parallelization strategy), and
  the terminal `## GSTACK REVIEW REPORT`.

## Step 0 is genuinely different content from Step 14's Step 0

Step 14's Step 0 is mode selection (SCOPE EXPANSION / SELECTIVE EXPANSION /
HOLD SCOPE / SCOPE REDUCTION). Step 15's Step 0 is "Scope Challenge" — a
different procedure entirely: existing-code-leverage check, minimum-change
check, a complexity trigger (8+ files or 2+ new classes/services → mandatory
STOP before any section review begins), Search-Before-Building
(Layer 1/2/3 + EUREKA), TODOS.md cross-reference, completeness check, and a
distribution check (build/publish pipeline for new artifact types). No mode
framework at all. Wrote the step file to describe this accurately rather
than reusing Step 14's mode-selection language, which would have been wrong.

## Plan file continuity — genuine open item, not resolved by source alone

[[[pdlf:app-factory/phase-b-discover-and-define/b15-reference|/plan-eng-review]]](C:/pdlf/app-factory/phase-b-discover-and-define/b15-reference.md) appends its review report to "the active plan file in
this conversation," detected via host-provided plan-mode signals — not a
GStack-managed lookup by `$SLUG`. Whether OpenCode's invocation of a GStack
skill presents an "active plan file" in the sense this check expects is not
confirmed by anything in either skill's source. Two sub-cases:

- Step 14 ran EXPANSION/SELECTIVE EXPANSION → a real GStack-native file
  exists and is the most likely candidate for whatever detection means here.
- Step 14 ran HOLD SCOPE/REDUCTION → no GStack-native file exists at all;
  only the orchestrator's own transcript capture. Whether [[[pdlf:app-factory/phase-b-discover-and-define/b15-reference|/plan-eng-review]]](C:/pdlf/app-factory/phase-b-discover-and-define/b15-reference.md)
  treats a pasted transcript as "the plan file" for its append-in-place
  mechanic is unconfirmed.

Resolution for now: the orchestrator's own `gstack-outputs\` copy step
(item 14) does not depend on the skill having written anywhere on disk —
it captures the review's findings from the skill's output regardless of
whether the skill's own file-write silently no-ops. Flagged as something to
watch on the first live run rather than a blocker on this step file.

## Outside Voice — new finding, applies to both Step 14 and Step 15

Confirmed to exist for both skills (independent AI-model review, offered
after all sections complete, default-on, informational, never gates
shipping). Neither this step's prior drafts nor Step 14's ever accounted for
it. Decision made here: leave it as GStack's own default behavior, don't
override or disable it, don't give it its own PDLF-tracked artifact — its
accepted findings land in the plan file like any other finding. Worth
revisiting whether Step 14 needs a matching note, since the mechanism is
identical there.

## Local/global conflict check — same conclusion as Step 14, reconfirmed

[[[pdlf:app-factory/phase-b-discover-and-define/b15-reference|/plan-eng-review]]](C:/pdlf/app-factory/phase-b-discover-and-define/b15-reference.md)'s `SKILL.md` has zero reference to `project-library-global`
— same as [[[pdlf:app-factory/phase-b-discover-and-define/b14-reference|/plan-ceo-review]]](C:/pdlf/app-factory/phase-b-discover-and-define/b14-reference.md). Confirms (doesn't just assume by symmetry) that
the conflict check is OpenCode's own comparison at both Step 14 and Step 15,
not something either skill surfaces.

## Open, not yet decided

- **`TODOS.md` path unconfirmed.** Assumed `dev-{slug}\{slug}-project-library\TODOS.md`
  (root-of-docs-repo level) pending developer confirmation. Not in
  [[[default:specifications-global/spec-nomenclature|Spec: Nomenclature]]](C:/dev/project-library-global/specifications-global/spec-nomenclature.md) yet — add it there once confirmed.
- **Plan file continuity** (above) — genuinely open, may only resolve on a
  live run.
- Whether Step 16's own skill source needs the same direct-read treatment
  Steps 14 and 15 got, before its step file is rebuilt — almost certainly
  yes, given the pattern so far.

## Global conventions applied throughout

- No `<project-library>` placeholder — `dev-{slug}\{slug}-project-library` in
  prose, full absolute path in any literal command
- No automatic git operations anywhere — every commit/push is asked
- No automatic memory-governor submission — asked, via the `mb-submit-memory` skill only
- No Step 13 references anywhere in this file
- No "Branch A/B" language — described plainly instead
- Naming follows [[[default:specifications-global/spec-nomenclature|Spec: Nomenclature]]](C:/dev/project-library-global/specifications-global/spec-nomenclature.md)'s Stepwise File Naming table: bare
  `step-15-` prefix on build notes and decision tree, skill name only in the
  step file's own filename

## Later decisions

1. **`[[15-plan-eng-review]]` was rebuilt in full, 2026-08-25.** The real step file
   had never actually been brought in line with this build notes file's own
   corrections — it still claimed the five-document TDD cluster this file already
   states is false, still used the `<project-library>` placeholder this file's own
   conventions rule out, and its "Task Execution Order" was three vague lines instead
   of the real, detailed procedure this file and the decision tree already establish.
   The rebuild carries every correction already recorded above directly into the real
   step file: no five-document cluster, the one genuine Test Plan Artifact, the full
   Scope Challenge sequence, all four review sections with per-finding
   `AskUserQuestion` discipline, Required Outputs written into the plan file, Outside
   Voice, and the terminal GSTACK REVIEW REPORT.
2. **`/sync-gbrain` replaced with the `mb-submit-memory` skill, submitting through the
   memory governor, as part of the same rebuild.** Same system-wide change as Steps 11,
   12, and 14 (master task list, items 9.2 and 9.4, which names
   `[[15-plan-eng-review]]` directly). Both of this step's real stable-copy
   artifacts — `gstack-outputs\step-15-eng-plan.md` and
   `gstack-outputs\step-15-test-plan.md` — are submitted individually, each its own
   separate call.
3. **`gbrain dream` and `gbrain eval suspected-contradictions` added to end-of-step
   housekeeping.** Master task list, item 9.8 — applies to every step. Run for real,
   never as a dry run. `gbrain eval suspected-contradictions` does not run
   automatically as part of `gbrain dream` and must be invoked as its own separate
   command every time.
4. **`mb-submit-memory` skill built and installed, 2026-08-25.** Same skill used at
   Steps 11, 12, and 14 — queries GBrain for related content, forms a real confidence
   score and contradiction judgment using a concrete, bounded method, reports its
   findings, and only submits after explicit developer approval. See the skill's own
   file for the full procedure.

## From `pdlf-build-plan.md`: step entry

### Phase B — Discover and Define

Ends with the gate `domain-locked` (Step 16).

#### Step 15: Engineering review

**Must achieve:** the plan's architecture, code quality, test coverage and performance locked, and a concrete test plan produced for the build steps.

**Starts from:** Step 14's plan; both design docs; the `/office-hours` result, if any; `project-library-global`.

**Produces:** the reviewed plan and the test plan, with stable copies in the project. The test plan is used later by Steps 35 and 38.

**Carried out by:** GStack `/plan-eng-review`.

**Must be built so that:**
- Step 14's plan is found according to the scope mode used, and pasted into the skill in full with the design docs and the same statement that a design doc already exists;
- OpenCode makes the same comparison with `project-library-global` as at Step 14;
- the skill's scope challenge stops for the developer when the plan is large (8 or more files, or 2 or more new services);
- each finding in the four reviews (architecture, code quality, tests, performance) is put to the developer one at a time;
- the second opinion from another AI is informational only: nothing from it is adopted without the developer's approval;
- the findings are captured by OpenCode itself, so the step does not depend on the skill finding a plan file to write into.

**BFT level:** Full.

## From `pdlf-phase-b-review.md`: findings for this step

## Purpose

This document reviews Phase B of PDLF (Steps 11, 12, 14, 15 and 16) as a case study, before Phases C to F are built. It looks at what was done wrong, what could have been done better, how Phase B should be corrected, and how the method should change for Phase C. It judges Phase B against `pdlf-intent.md`, against the principles of mybizz-os, and against the skills catalogue. It is not a plan for Phase C.

The evidence is the five step files, their build notes and decision trees, the build plan, the built report, the old `workflow.md`, the old step mapping, and `skills-catalog.md`.

## 1. What we did wrong

**1.1 We built the steps before we had stated the intent.** The order was step file first, build notes second and intent last. Every step therefore carries assumptions that the intent later reversed: housekeeping questions at the end of every step, a ledger with six tables, a project registry and a project inventory that no longer exist, makePDLF paths and prefixes, the devlog and judgement trail, and the old rule "use a skill only when it beats OpenCode". None of these were careless; they were right when written and became wrong when the intent was settled. The cost is that all five steps now need repair before they can be packaged.

**1.2 We called the steps "built" without ever running them.** Not one of the five steps has been run against a real application. Several open questions can only be answered by a run: whether `/plan-eng-review` finds "the active plan file" inside OpenCode, where `TODOS.md` belongs, and whether the statement that "a design doc already exists" really stops GStack from re-offering `/office-hours`. mybizz-os's own principle is "present is not working, and completed is not worked". By that principle, Phase B is designed, not built.

**1.3 Each step repeats the rules that apply to every step.** Every step file spells out, in its own words, the GBrain search, the ledger row, the Step Receipt, the BFT, the two housekeeping questions and a five-action memory sequence. The same rule is written five times, slightly differently each time, so one change (such as moving close-out to `/mb-close-out`) has to be made in five places and is easily missed in one. This breaks "one fact, one home".

**1.4 Each step ran its own memory and dream cycle.** The housekeeping asked, at every step, to run `gbrain dream` and `gbrain eval suspected-contradictions`. In mybizz-os, the dream cycle is a long, heavy process run on Sundays after the diagnostic, with a manual review afterwards. Running it after every step would have cost hours across a build and buried the developer in reviews. The intent's close-out rule replaces this.

**1.5 We wrapped outside skills without first reading them.** Three steps were designed from a skill's name or summary and were wrong: Step 15 assumed five architecture documents that the skill never produces; Step 16 invoked `/domain-modeling`, which cannot run on its own; and Step 14 used the wrong GStack save path. Each mistake was caught later, by reading the skill's source, and written down as a lesson in the build notes, three times over. The lesson was never turned into a rule before the next step was designed.

**1.6 Lessons went into build notes, where nobody reads them.** Each step's build notes end with "Learnings". The intent says a lesson is written into the source that the next build reads. The build notes are not that source: they are history. The lessons from Phase B ("read the skill's source first", "paste context into the skill, because it does not read our folders", "state file destinations explicitly") belong in the build plan's rules.

**1.7 Anvil and our own standards are almost absent from Phase B.** The intent's second success criterion is that Anvil's standards are applied throughout. Phase B locks the architecture (Step 15) and the domain model (Step 16) without once using Anvil's own skills. The catalogue's Anvil skill `data-models` says it should be used "before choosing an architecture for persisted domain data", which is exactly what Steps 15 and 16 do. Likewise, the only use of `project-library-global` is a vague "local/global conflict check"; no step names which standard it applies.

**1.8 The non-negotiable rules are not given to the skills.** The intent says AI agents are given the no-multi-tenancy rule as context before any code is generated, because they reach for shared databases by default. Steps 12, 14 and 15 shape the architecture through generic GStack skills, and none of them is given the five-app structure, the no-multi-tenancy decision or the Material 3 design standard. A generic architecture review is exactly where a shared-database design would be proposed.

## 2. What we could have done better

**2.1 Too many documents per step.** Each step has a step file, build notes and a decision tree, and was also described in `workflow.md` and the step mapping. That is five places for one step, and they drifted apart. The decision trees are hand-written pictures of the step's action list, so they are a second copy of it. One step file, one build-plan entry and one built-report entry are enough.

**2.2 The reviews overlap, and every overlap costs the developer questions.** Step 14's CEO review has eleven sections, including architecture, security, data flow, tests and performance. Step 15's engineering review covers architecture, code quality, tests and performance again. Both put every finding to the developer as a separate question. That is the right discipline, but asked twice about the same subjects, the developer faces a very long run of questions, and a tired reviewer is the rubber-stamp that BFT exists to prevent. Each review should have its own remit, so that no subject is reviewed twice.

**2.3 Generic review content does not fit Anvil.** The GStack reviews were written for general web development. Parts of them have no meaning for an Anvil application: build and publish pipelines, worktree parallelisation, N+1 query patterns written for other frameworks. Without Anvil context, the reviews ask about things that do not apply and miss things that do.

**2.5 Skill choices were made step by step, not from the catalogue.** Each step picked the skill that came to mind. The catalogue was never read as a whole to ask: which installed skill best serves this step, and which skill is installed but unused?

## 3. How Phase B should be corrected

1. **Bring all five steps into line with the intent's rules:** close-out by `/mb-close-out`, the agent never commits, seven ledger tables, no registry or inventory, artifact copies to `C:\pdlf\output\`, no devlog or judgement trail, skills take precedence.

2. **Remove the repeated rules from the step files.** Each step file states only what is particular to it and points to the rules every step follows.

3. **Give every skill a standard context pack** at invocation: the five-app structure, the no-multi-tenancy decision, the Material 3 design standard, and the `project-library-global` standards the step applies.

4. **Add Anvil's `data-models` skill to Steps 15 and 16,** where the architecture and the domain model are fixed.

5. **Add `secure-software-engineering` to Steps 14 and 15,** where security requirements and the threat model belong. That skill is for prevention during requirements and design, which is earlier than Sentinel's review at Step 16.

7. **Give Steps 14 and 15 separate remits:** Step 14 settles scope and ambition; Step 15 settles architecture, tests and performance. Neither reviews the other's subjects.

9. **Run Phase B on the test application** (the Daily Intentions Tracker in `mb5pdlf`), answer the open questions from the run, and only then record the steps as finished.

10. **Move the lessons out of the build notes** into the build plan's rules, then retire the build notes and decision trees.

## From `spec-artifact-handover.md`: watched item 1

| # | Item | Status |
|---|---|---|
| 1 | Built steps 14–15: legacy `gstack-outputs\` folder name; missing `{slug}-` copy prefix; stale quote of an older skill generation's `~/.claude` path in Step 14's description (current skill source verified clean 2026-09-11) | Correction tracked — master task list, item 18 |
