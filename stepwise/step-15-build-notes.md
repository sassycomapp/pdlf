---
title: "step-15-build-notes"
doc-id: "mb-3791a43c"
updated: "2026-10-12"
---
# Step 15 (plan-eng-review) — Build Notes

Captured during discussion, before this step file was rebuilt. Points to carry forward.

## Task list (matches [[[makepdlf-project-library:stepwise/step-15-plan-eng-review|step-15-plan-eng-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-15-plan-eng-review.md))

1. Query GBrain (automatic, read-only) — sources explicitly nominated
2. Check Step 14's mode/ledger row to determine which plan artifact exists
3. Assemble context: plan artifact, design doc, first-concept draft, [[[makepdlf-project-library:stepwise/step-12-office-hours|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md) output
4. Local/global conflict check — same OpenCode-run mechanics as Step 14
5. Invoke [[[makepdlf-project-library:stepwise/step-15-plan-eng-review|/plan-eng-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-15-plan-eng-review.md), pasting everything, stating a design doc already exists
6–12. Skill runs: pre-review audit → Step 0 (Scope Challenge) → 4-section review →
   Test Plan Artifact write → Required Outputs → Outside Voice → GSTACK REVIEW REPORT
13–15. Capture and copy both artifacts; verify
16–22. Ledger row, Step Receipt, BFT Full, housekeeping, present, continue

## Correction — the five-document TDD cluster was never real

Every prior draft of this step (including the one carried into
`docs-local/todo-makepdlf.md` §3.2, marked `[COMPLETE 2026-07-10]`) assumed
[[[makepdlf-project-library:stepwise/step-15-plan-eng-review|/plan-eng-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-15-plan-eng-review.md) produces five separate documents: [[[mb-3-cs-project-library:docs-local/architecture|architecture]]](C:/dev/dev-mb-3-cs/mb-3-cs-project-library/docs-local/architecture.md) (mb-3-cs project library),
[[[mb-3-cs-project-library:docs-standard-local/integration-architecture|integration-architecture]]](C:/dev/dev-mb-3-cs/mb-3-cs-project-library/docs-standard-local/integration-architecture.md) (mb-3-cs project library), the retired `security-architecture-canonical.md`,
[[[mb-3-cs-project-library:docs-standard-local/globals-contract|globals-contract]]](C:/dev/dev-mb-3-cs/mb-3-cs-project-library/docs-standard-local/globals-contract.md) (mb-3-cs project library), [[[mb-3-cs-project-library:docs-local/authoritative-schema|authoritative-schema]]](C:/dev/dev-mb-3-cs/mb-3-cs-project-library/docs-local/authoritative-schema.md) (mb-3-cs project library). Read [[[makepdlf-project-library:stepwise/skill-source-reference/plan-eng-review-review-sections|Plan Eng Review Review Sections]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/skill-source-reference/plan-eng-review-review-sections.md)
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
  Critical Paths). Consumed automatically by [[[makepdlf-project-library:stepwise/step-38-qa|/qa]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-38-qa.md) and `/qa-only` — confirmed
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

[[[makepdlf-project-library:stepwise/step-15-plan-eng-review|/plan-eng-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-15-plan-eng-review.md) appends its review report to "the active plan file in
this conversation," detected via host-provided plan-mode signals — not a
GStack-managed lookup by `$SLUG`. Whether OpenCode's invocation of a GStack
skill presents an "active plan file" in the sense this check expects is not
confirmed by anything in either skill's source. Two sub-cases:

- Step 14 ran EXPANSION/SELECTIVE EXPANSION → a real GStack-native file
  exists and is the most likely candidate for whatever detection means here.
- Step 14 ran HOLD SCOPE/REDUCTION → no GStack-native file exists at all;
  only the orchestrator's own transcript capture. Whether [[[makepdlf-project-library:stepwise/step-15-plan-eng-review|/plan-eng-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-15-plan-eng-review.md)
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

[[[makepdlf-project-library:stepwise/step-15-plan-eng-review|/plan-eng-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-15-plan-eng-review.md)'s `SKILL.md` has zero reference to `project-library-global`
— same as [[[makepdlf-project-library:stepwise/step-14-plan-ceo-review|/plan-ceo-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-14-plan-ceo-review.md). Confirms (doesn't just assume by symmetry) that
the conflict check is OpenCode's own comparison at both Step 14 and Step 15,
not something either skill surfaces.

## Open, not yet decided

- **`TODOS.md` path unconfirmed.** Assumed `dev-{slug}\{slug}-project-library\TODOS.md`
  (root-of-docs-repo level) pending developer confirmation. Not in
  [[[makepdlf-project-library:specifications-local/spec-nomenclature|Spec: Nomenclature]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-nomenclature.md) yet — add it there once confirmed.
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
- Naming follows [[[makepdlf-project-library:specifications-local/spec-nomenclature|Spec: Nomenclature]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-nomenclature.md)'s Stepwise File Naming table: bare
  `step-15-` prefix on build notes and decision tree, skill name only in the
  step file's own filename

## Later decisions

1. **`[[step-15-plan-eng-review]]` was rebuilt in full, 2026-08-25.** The real step file
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
   `[[step-15-plan-eng-review]]` directly). Both of this step's real stable-copy
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
