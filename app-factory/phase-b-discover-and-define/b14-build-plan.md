---
title: "b14-build-plan"
doc-id: "mb-4d5937f5"
updated: "2026-10-13"
---

## From `14-build-notes.md`

# Step 14 (plan-ceo-review) — Build Notes

Captured during discussion, before this step file was rebuilt. Points to carry forward.

## Task list (matches `14-plan-ceo-review.md`)

1. Query GBrain (automatic, read-only) — sources explicitly nominated:
   `{slug}`, `{slug}-project-library`, `project-library-global`
2. Check Step 12's `synthesized` flag — determines whether item 5's design-doc
   preemption is load-bearing or redundant
3. Assemble Step 12's four-artifact handoff into context (design doc, first-concept
   draft, [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md) output if it ran, Step 12 Step Receipt)
4. Local/global conflict check — global wins by default, deviation request to diverge
5. Invoke [[[pdlf:app-factory/phase-b-discover-and-define/b14-reference|/plan-ceo-review]]](C:/pdlf/app-factory/phase-b-discover-and-define/b14-reference.md), pasting all four artifacts in full, stating explicitly
   that a design doc already exists
6. Skill runs pre-review system audit → Step 0 (mode selection) → 11-section review
7. Mode-dependent output capture (see below)
8–9. Capture and copy the plan artifact to `gstack-outputs\step-14-ceo-plan.md`
10. Verify outputs exist; deviation request if missing
11–13. Ledger row, Step Receipt, BFT Full
14. Explain, present the Step Receipt, stop and ask David to run `/mb-close-out`
15. Ask to continue

## Core principle — no branch on Step 12's provenance

Step 12 always hands off the same four artifacts regardless of whether
[[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md) ran. Step 14 always pastes all four into the [[[pdlf:app-factory/phase-b-discover-and-define/b14-reference|/plan-ceo-review]]](C:/pdlf/app-factory/phase-b-discover-and-define/b14-reference.md)
prompt, in full text, before invoking it — never relies on the skill's own
design-doc glob. This mirrors Step 12's own handling of [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md).

Explicitly rejected during this build: the old draft's Branch A ("no design doc
found") / Branch B ("design doc found") split. That framing assumed the skill's
internal detection determines the procedure. It doesn't — the orchestrator's own
handoff does. One procedure, not two.

## Skill-source findings — confirmed, not assumed

`SKILL.md` and `SKILL.md.tmpl` for [[[pdlf:app-factory/phase-b-discover-and-define/b14-reference|/plan-ceo-review]]](C:/pdlf/app-factory/phase-b-discover-and-define/b14-reference.md) were read directly (not
inferred from Plan Eng Review Review Sections/`manifest.json` alone, which only cover the
11-section review gated behind Step 0). Three findings changed what the old
draft assumed:

1. **GStack-native plan path uses `sassycomapp-{slug}-project-library`, not
   bare `{slug}`.** `$SLUG` resolves via `~/.claude/skills/gstack/bin/gstack-slug`
   (falling back to the git toplevel's basename). This is the same resolution
   [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md) uses, and matches the form already confirmed in
   `project-inventory.md` for every registered project's GStack path. The old
   draft's `~/.gstack/projects/{slug}/ceo-plans/...` was the exact same class of
   error already caught once for [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md)'s design-doc path — caught
   again here by reading source instead of carrying the assumption forward.

2. **The skill runs its own design-doc glob regardless of what's pasted into
   the prompt**, and if it comes up empty (Step 12 declined [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md),
   `synthesized = true`), the skill's own "Prerequisite Skill Offer" fires —
   asking the developer, inside Step 14, whether to run [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md) inline.
   That would silently reopen a decision Step 12 already closed. This is why
   item 5 explicitly states in the invocation that a design doc already exists:
   not stylistic, load-bearing — it's the only thing that suppresses the
   re-offer.

3. **Plan-file persistence is mode-dependent.** Confirmed in `SKILL.md` §
   "0D-POST. Persist CEO Plan (EXPANSION and SELECTIVE EXPANSION only)" — HOLD
   SCOPE and SCOPE REDUCTION write nothing to `ceo-plans/`. This wasn't in
   either prior draft. Step 14 now branches its output-capture step: copy the
   GStack-native file for the two expansion modes, orchestrator-saves the
   conversational transcript for the other two.

## Local/global conflict check — mechanics resolved

[[[pdlf:app-factory/phase-b-discover-and-define/b14-reference|/plan-ceo-review]]](C:/pdlf/app-factory/phase-b-discover-and-define/b14-reference.md)'s `SKILL.md` has zero reference to `project-library-global`
anywhere in source. The conflict check is confirmed to be entirely OpenCode's
own structured comparison, run alongside the skill invocation — not something
the skill surfaces on its own. This closes the "not yet verified" item carried
in the original `step-14-build-notes.md`.

Still open, per [[[pdlf:pdlf-library/adr-local/project-library-global-registration|Project Library Global Registration]]](C:/pdlf/pdlf-library/adr-local/project-library-global-registration.md): exactly
where PDLF verifies `project-library-global` itself is registered and
queryable (Step 11 check vs. separate bootstrap procedure). Step 14 treats a
missing registration as a deviation request, not a silent skip, but does not
resolve where that check belongs.

## Learnings

- **Reading a skill's `SKILL.md` directly, not just its section manifest,
  matters.** `manifest.json` + Plan Eng Review Review Sections alone would have left the
  design-doc preemption requirement, the mode-dependent persistence split, and
  the correct GStack path all unverified. All three were only findable in the
  actual `SKILL.md`.
- **"Never rely on the skill's internal detection" and "the skill runs its own
  detection anyway" are not in tension.** The orchestrator's paste is not a
  replacement for the skill's own audit — it's an explicit override, stated in
  the prompt, that prevents the audit's failure path (no design doc found) from
  triggering an unwanted re-ask. Both things are true at once.
- Ledger substep 11 rewritten against the real [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md)
  schema — `step_number`, `type`, `status`, `synthesized`, `artifact_path` are
  real columns, not assumed field names.

## Open, not yet decided

- Whether Step 15's [[[pdlf:app-factory/phase-b-discover-and-define/b15-reference|/plan-eng-review]]](C:/pdlf/app-factory/phase-b-discover-and-define/b15-reference.md) has the same mode-dependent persistence
  behavior, or always writes a file regardless of Step 14's mode. Not yet
  checked against [[[pdlf:app-factory/phase-b-discover-and-define/b15-reference|/plan-eng-review]]](C:/pdlf/app-factory/phase-b-discover-and-define/b15-reference.md)'s own `SKILL.md` — carry this question
  into that step's rebuild.
- Exact format of the "explicit design-doc-exists" statement in the invocation
  prompt (item 5) — a fixed template sentence, or freeform framing left to the
  orchestrator's judgment at invocation time? Not yet decided.

## Global conventions applied throughout

- No `<project-library>` placeholder — use `dev-{slug}\{slug}-project-library`
  in prose, full absolute path in any literal command
- The agent never commits or pushes. Every step ends by explaining what was done, stopping and asking David to run `/mb-close-out`.
- No Step 13 references anywhere in this file — purged per the handover's
  explicit requirement
- No "Branch A/B" language — described plainly instead

## From `pdlf-build-plan.md`: step entry

### Phase B — Discover and Define

Ends with the gate `domain-locked` (Step 16).

#### Step 14: CEO review

**Must achieve:** the design's scope and ambition challenged and settled, with the developer choosing how far the scope goes; the result is the CEO plan, which also names what must be tested and why.

**Starts from:** the four items handed over by Step 12; `project-library-global`.

**Produces:** the CEO plan, with a stable copy in the project.

**Carried out by:** GStack `/plan-ceo-review`.

**Must be built so that:**
- all four items from Step 12 are pasted into the skill in full, whatever route Step 12 took, with a plain statement that a design doc already exists, so that the skill does not reopen Step 12's decision by offering `/office-hours` again;
- before the skill runs, OpenCode compares what the review touches with `project-library-global`: the global standard wins unless the developer approves a deviation;
- the developer chooses the scope mode (expansion, selective expansion, hold scope or reduction), and every finding is put to the developer one at a time, never in a batch;
- the plan is captured in every mode: the skill saves it itself only in the two expansion modes, so in the other two OpenCode saves it;
- Step 12's input notice is carried forward if its design doc was synthesized;
- the security review `mb-sentinel-review` runs on the step's output at Medium scrutiny, against the documents Sentinel names for Step 14; a Flag or Escalate stops the step and goes to the developer; before the step finishes, its `triage_findings` row is checked, so that the review's run is proven, not assumed;
- the `secure-software-engineering` skill, given the context pack, writes the security requirements at the level of the business into the CEO plan: what data the app holds, whose it is, who may see or change it, and what must never leak.

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

**1.5 We wrapped outside skills without first reading them.** Three steps were designed from a skill's name or summary and were wrong: Step 15 assumed five architecture documents that the skill never produces; Step 16 invoked `/domain-modeling`, which cannot run on its own; and Step 14 used the wrong GStack save path. Each mistake was caught later, by reading the skill's source, and written down as a lesson in the build notes, three times over. The lesson was never turned into a rule before the next step was designed.

**1.6 Lessons went into build notes, where nobody reads them.** Each step's build notes end with "Learnings". The intent says a lesson is written into the source that the next build reads. The build notes are not that source: they are history. The lessons from Phase B ("read the skill's source first", "paste context into the skill, because it does not read our folders", "state file destinations explicitly") belong in the build plan's rules.

**1.8 The non-negotiable rules are not given to the skills.** The intent says AI agents are given the no-multi-tenancy rule as context before any code is generated, because they reach for shared databases by default. Steps 12, 14 and 15 shape the architecture through generic GStack skills, and none of them is given the five-app structure, the no-multi-tenancy decision or the Material 3 design standard. A generic architecture review is exactly where a shared-database design would be proposed.

## 2. What we could have done better

**2.1 Too many documents per step.** Each step has a step file, build notes and a decision tree, and was also described in `workflow.md` and the step mapping. That is five places for one step, and they drifted apart. The decision trees are hand-written pictures of the step's action list, so they are a second copy of it. One step file, one build-plan entry and one built-report entry are enough.

**2.2 The reviews overlap, and every overlap costs the developer questions.** Step 14's CEO review has eleven sections, including architecture, security, data flow, tests and performance. Step 15's engineering review covers architecture, code quality, tests and performance again. Both put every finding to the developer as a separate question. That is the right discipline, but asked twice about the same subjects, the developer faces a very long run of questions, and a tired reviewer is the rubber-stamp that BFT exists to prevent. Each review should have its own remit, so that no subject is reviewed twice.

**2.3 Generic review content does not fit Anvil.** The GStack reviews were written for general web development. Parts of them have no meaning for an Anvil application: build and publish pipelines, worktree parallelisation, N+1 query patterns written for other frameworks. Without Anvil context, the reviews ask about things that do not apply and miss things that do.

**2.4 The biggest commitments in Phase B are not gated.** Phase B's only gate is at Step 16. Yet the concept (Step 12) and the scope (Step 14) are the commitments everything else rests on. They are approved inside their steps, but not as gates, and the concept is only locked formally at Step 21.

**2.5 Skill choices were made step by step, not from the catalogue.** Each step picked the skill that came to mind. The catalogue was never read as a whole to ask: which installed skill best serves this step, and which skill is installed but unused?

## 3. How Phase B should be corrected

1. **Bring all five steps into line with the intent's rules:** close-out by `/mb-close-out`, the agent never commits, seven ledger tables, no registry or inventory, artifact copies to `C:\pdlf\output\`, no devlog or judgement trail, skills take precedence.

2. **Remove the repeated rules from the step files.** Each step file states only what is particular to it and points to the rules every step follows.

3. **Give every skill a standard context pack** at invocation: the five-app structure, the no-multi-tenancy decision, the Material 3 design standard, and the `project-library-global` standards the step applies.

5. **Add `secure-software-engineering` to Steps 14 and 15,** where security requirements and the threat model belong. That skill is for prevention during requirements and design, which is earlier than Sentinel's review at Step 16.

7. **Give Steps 14 and 15 separate remits:** Step 14 settles scope and ambition; Step 15 settles architecture, tests and performance. Neither reviews the other's subjects.

8. **Decide whether the concept needs its own gate** at the end of Step 12.

9. **Run Phase B on the test application** (the Daily Intentions Tracker in `mb5pdlf`), answer the open questions from the run, and only then record the steps as finished.

10. **Move the lessons out of the build notes** into the build plan's rules, then retire the build notes and decision trees.

## From `spec-artifact-handover.md`: watched item 1

| # | Item | Status |
|---|---|---|
| 1 | Built steps 14–15: legacy `gstack-outputs\` folder name; missing `{slug}-` copy prefix; stale quote of an older skill generation's `~/.claude` path in Step 14's description (current skill source verified clean 2026-09-11) | Correction tracked — master task list, item 18 |
