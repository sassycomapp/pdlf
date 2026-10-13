---
title: "b12-build-plan"
doc-id: "mb-19064cbb"
updated: "2026-10-13"
---

## From `12-build-notes.md`

# Step 12 — Build Notes: Full Task List

## Task list (matches [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|12-office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md))

1. Query GBrain (automatic, read-only)
2. Branch on entry mode, determined at Step 11

**New-project entry:**
3. Read the three pre-project docs from `dev-{slug}\{slug}-project-library\pre-project\`
4. Query the developer diligently, from scratch — loop until scope is adequately
   described

**Existing-project entry:**
3e. Read the whole existing project-library via GBrain — identify canonical (durable
    concept) vs. consequential (things that followed from it)
4e. If an existing document already claims to state the concept (old `design-doc.md`,
    `CONTEXT.md`, etc.), surface it explicitly — never fold it silently into the read
5e. Propose the canonical/consequential split, side by side with anything surfaced at
    4e. Developer confirms or corrects — propose-and-confirm, not from-scratch
    interrogation

**Both converge:**
6. Synthesize a design doc (always — not conditional on the [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md) decision):
   Problem Statement, Demand Evidence, Status Quo, Target User & Narrowest Wedge,
   Constraints, Approaches Considered, Recommended Approach, Open Questions, Success
   Criteria. For existing-project entry, this represents the redeveloped concept, built
   from what was identified as canonical — not a copy of consequential material.
7. Save the draft to two files: `design-doc-first-concept.md` (permanent, never
   overwritten again) and `design-doc.md` (working copy)
8. Ask the developer: run [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md)? (yes/no)

**If declined:** ledger `synthesized = true`; downstream INPUT NOTICE.

**If accepted:** pre-load the source material (pre-project docs or the
propose-and-confirm result) and the full text of `design-doc-first-concept.md` into the
[[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md) prompt — recognized as a fully formed plan, so it skips the interview
but still runs Premise Challenge and Alternatives. Invoke [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md). Capture its
GStack-native output path. Copy that file over `design-doc.md` (working copy only —
first-concept file untouched). Ledger `synthesized = false`. Never move the
GStack-native file.

**Both paths converge:**

9. Verify `design-doc.md` exists (and GStack path, if [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md) ran)
10. If missing: deviation request
11. Write ledger row
12. Save Step Receipt to `dev-{slug}\{slug}-project-library\pdlf\step-12-receipt.md`
13. Apply BFT — Full
14. Explain what was done and why, present the Step Receipt, stop and ask David to run `/mb-close-out`
15. Ask: continue to Step 14?

**Handoff:** Step 14 must run, taking into context together: `design-doc.md`,
`design-doc-first-concept.md`, the [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md) output file (if it ran), and the
Step 12 Step Receipt. The first-concept file is a fourth artifact added during drafting
— flagged in the step file itself, not silently assumed.

## Core principle — existing-project entry

Submitting an existing project to PDLF means redeveloping it around its canonical
concept, not auditing, maintaining, or correcting what already exists. PDLF is a
development system, not a refactoring system. This principle also retired the
disposition-audit model entirely (`step-02-existing-registration.md`,
`step-03-resume-point-audit.md`, the retired `sop-existing-project-resume-audit.md` — all removed).
Every step always runs, for every project. What differs for an existing project is only
the material a step starts from, never whether the step runs.

## Learnings

- **[[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md) accepts a pre-written draft, confirmed from the actual skill file
  (not assumed).** It has a built-in "fully formed plan" path: if given one, it skips
  the interview questions but still forces the draft through Premise Challenge and
  Alternatives — pressure-tested, not rubber-stamped.
- **The draft must be pasted into the invocation prompt itself**, not just saved to a
  file. [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md)'s own Phase 1 does not scan our project folder — it only reads
  `CLAUDE.md`, `TODOS.md`, git history, and its own native design-doc history at
  `~/.gstack/projects/sassycomapp-dev-{slug}\{slug}-project-library/*-design-*.md`. None of those is our
  `docs-local\design-doc.md`.
- GStack-native save path confirmed correct against the actual skill file:
  `~/.gstack/projects/sassycomapp-dev-{slug}\{slug}-project-library/{user}-{branch}-design-{datetime}.md`.

## Global conventions applied throughout

- No `<project-library>` placeholder — use `dev-{slug}\{slug}-project-library` in prose, full
  absolute path in any literal command
- The agent never commits or pushes. Every step ends by explaining what was done, stopping and asking David to run `/mb-close-out`.

## From `pdlf-build-plan.md`: step entry

### Phase B — Discover and Define

Ends with the gate `domain-locked` (Step 16).

#### Step 12: Office hours

**Must achieve:** the application's design doc: what problem it solves, for whom, and how, stated well enough for every later step to build on.

**Starts from:** for a new application, the three pre-project files; for an existing application, its whole existing documentation, read through GBrain.

**Produces:** `docs-local\design-doc-first-concept.md`, written once and never changed afterwards, kept to check later for concept drift; `docs-local\design-doc.md`, the working copy; the `/office-hours` result, if it ran.

**Carried out by:** OpenCode, with GStack `/office-hours` if the developer chooses.

**Must be built so that:**
- for a new application, the agent questions the developer until the scope is adequately described;
- for an existing application, the agent separates the durable concept from what merely followed from it, shows plainly any document that already claims to state the concept, and proposes the split for the developer to confirm or correct; the application is redeveloped around its concept, not audited;
- the design doc is always written, in a fixed structure (problem, demand, status quo, target user, constraints, approaches, recommendation, open questions, success criteria), before `/office-hours` is offered;
- if the developer accepts `/office-hours`, the full draft is pasted into it, so that it skips its interview but still challenges the premise and the alternatives; its result becomes the working copy, and its own file is never moved;
- the ledger records whether the design doc was synthesized without `/office-hours`, so that later steps carry an input notice;
- it hands four items to Step 14: both design docs, the `/office-hours` result if any, and its Step Receipt.

**BFT level:** Full.

**References:** [[[pdlf:pdlf-library/policy-local/pol-step-conditional-state|Step Conditional State Policy]]](C:/pdlf/pdlf-library/policy-local/pol-step-conditional-state.md).

## From `pdlf-phase-b-review.md`: findings for this step

## Purpose

This document reviews Phase B of PDLF (Steps 11, 12, 14, 15 and 16) as a case study, before Phases C to F are built. It looks at what was done wrong, what could have been done better, how Phase B should be corrected, and how the method should change for Phase C. It judges Phase B against `pdlf-intent.md`, against the principles of mybizz-os, and against the skills catalogue. It is not a plan for Phase C.

The evidence is the five step files, their build notes and decision trees, the build plan, the built report, the old `workflow.md`, the old step mapping, and `skills-catalog.md`.

## 1. What we did wrong

**1.1 We built the steps before we had stated the intent.** The order was step file first, build notes second and intent last. Every step therefore carries assumptions that the intent later reversed: housekeeping questions at the end of every step, a ledger with six tables, a project registry and a project inventory that no longer exist, makePDLF paths and prefixes, the devlog and judgement trail, and the old rule "use a skill only when it beats OpenCode". None of these were careless; they were right when written and became wrong when the intent was settled. The cost is that all five steps now need repair before they can be packaged.

**1.2 We called the steps "built" without ever running them.** Not one of the five steps has been run against a real application. Several open questions can only be answered by a run: whether `/plan-eng-review` finds "the active plan file" inside OpenCode, where `TODOS.md` belongs, and whether the statement that "a design doc already exists" really stops GStack from re-offering `/office-hours`. mybizz-os's own principle is "present is not working, and completed is not worked". By that principle, Phase B is designed, not built.

**1.3 Each step repeats the rules that apply to every step.** Every step file spells out, in its own words, the GBrain search, the ledger row, the Step Receipt, the BFT, the two housekeeping questions and a five-action memory sequence. The same rule is written five times, slightly differently each time, so one change (such as moving close-out to `/mb-close-out`) has to be made in five places and is easily missed in one. This breaks "one fact, one home".

**1.6 Lessons went into build notes, where nobody reads them.** Each step's build notes end with "Learnings". The intent says a lesson is written into the source that the next build reads. The build notes are not that source: they are history. The lessons from Phase B ("read the skill's source first", "paste context into the skill, because it does not read our folders", "state file destinations explicitly") belong in the build plan's rules.

**1.8 The non-negotiable rules are not given to the skills.** The intent says AI agents are given the no-multi-tenancy rule as context before any code is generated, because they reach for shared databases by default. Steps 12, 14 and 15 shape the architecture through generic GStack skills, and none of them is given the five-app structure, the no-multi-tenancy decision or the Material 3 design standard. A generic architecture review is exactly where a shared-database design would be proposed.

**1.9 One step improvises where a skill exists.** Step 12 tells OpenCode to "query the developer diligently" until the scope is clear. The catalogue has a skill for exactly that, `grilling` (and `grill-me`), which Step 16 already uses. Under the intent's rule that skills take precedence, Step 12 should use it.

## 2. What we could have done better

**2.1 Too many documents per step.** Each step has a step file, build notes and a decision tree, and was also described in `workflow.md` and the step mapping. That is five places for one step, and they drifted apart. The decision trees are hand-written pictures of the step's action list, so they are a second copy of it. One step file, one build-plan entry and one built-report entry are enough.

**2.4 The biggest commitments in Phase B are not gated.** Phase B's only gate is at Step 16. Yet the concept (Step 12) and the scope (Step 14) are the commitments everything else rests on. They are approved inside their steps, but not as gates, and the concept is only locked formally at Step 21.

**2.5 Skill choices were made step by step, not from the catalogue.** Each step picked the skill that came to mind. The catalogue was never read as a whole to ask: which installed skill best serves this step, and which skill is installed but unused?

## 3. How Phase B should be corrected

1. **Bring all five steps into line with the intent's rules:** close-out by `/mb-close-out`, the agent never commits, seven ledger tables, no registry or inventory, artifact copies to `C:\pdlf\output\`, no devlog or judgement trail, skills take precedence.

2. **Remove the repeated rules from the step files.** Each step file states only what is particular to it and points to the rules every step follows.

3. **Give every skill a standard context pack** at invocation: the five-app structure, the no-multi-tenancy decision, the Material 3 design standard, and the `project-library-global` standards the step applies.

6. **Use `grilling` in Step 12** for questioning the developer, in place of the improvised interview.

8. **Decide whether the concept needs its own gate** at the end of Step 12.

9. **Run Phase B on the test application** (the Daily Intentions Tracker in `mb5pdlf`), answer the open questions from the run, and only then record the steps as finished.

10. **Move the lessons out of the build notes** into the build plan's rules, then retire the build notes and decision trees.

## From `pol-step-conditional-state.md`: Step 12 eligibility

### Step 12 — /office-hours (conditional, NOT test-mode-eligible)

Step 12 is a simple yes/no decision gate. The developer chooses:

- **Yes:** Run [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md) → `status = "complete"`, `synthesized = false`.
  Design doc produced by [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md).
- **No:** OpenCode synthesizes a design doc from the pre-project documents →
  `status = "complete"`, `synthesized = true`. Design doc produced by OpenCode.

Step 12 always produces a design document. The `synthesized` flag indicates
whether it came from [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md) or from OpenCode's synthesis. There is no
`skipped` state for Step 12 — the step always completes with an artifact.

There is no abbreviation offer for Step 12. The developer either runs the full
skill or OpenCode synthesizes from the pre-project docs.

## From `pol-step-conditional-state.md`: full mode

- Step 12: yes/no gate still applies (developer can decline [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md) and OpenCode synthesizes)

## From `pol-step-conditional-state.md`: full mode

- The `synthesized` flag can still be set for Step 12 (OpenCode synthesis when [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md) declined)

## From `spec-execution-discipline.md`: test-mode eligibility

When a project is in `test` mode, Step 20 is eligible for abbreviation. If the
developer chooses an abbreviated or skipped run, the step's `synthesized` flag is set to
`true` (abbreviated) or the step's `status` is set to `"skipped"` in the ledger.
Step 12 is a simple yes/no decision gate — not test-mode-eligible. See
`[[step-conditional-state-policy]]` for the full state definitions.
