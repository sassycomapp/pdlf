---
title: "b16-build-plan"
doc-id: "mb-625b446e"
updated: "2026-10-20"
---

## From `16-build-notes.md`

# Step 16 (domain-modeling) — Build Notes

## Correction 1 — wrong skill invoked in every prior draft

Old draft: "Run Matt [[[pdlf:app-factory/phase-b-discover-and-define/b16-reference|Step 16 Domain Modeling]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-reference.md) forward from Step 15's reviewed plan."
Confirmed against the real `SKILL.md` (mattpocock/skills,
`skills/engineering/domain-modeling/SKILL.md`): `/domain-modeling` has no
interview loop, no `AskUserQuestion`-equivalent sequence, no standalone
"run and get an artifact" shape. Its own description: "Use when the user
wants to pin down domain terminology... **or when another skill needs to
maintain the domain model**." It's infrastructure other skills call into.

Actual user-invocable skill: `/grill-with-docs`. Its entire `SKILL.md` body:
"Run a `/grilling` session, using the [[[pdlf:app-factory/phase-b-discover-and-define/b16-reference|/domain-modeling]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-reference.md) skill." `/grilling`
is the interview engine (it maps the decisions as a tree and asks every
question that can be asked at that point, in one round, each with a recommended
answer, then waits for the developer); [[[pdlf:app-factory/phase-b-discover-and-define/b16-reference|/domain-modeling]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-reference.md) fires inline during that
interview whenever a term needs sharpening or an ADR is warranted.

## Correction 2 — "reconciliation mode" had nothing left to attach to

Old draft branched on Step 3's disposition table (SKIP/RE-RUN/RUN-AS-NEW).
That model — and Step 3 itself — was retired system-wide this session
(session-decisions-and-learnings.md #2–4). Rather than reconstruct an
equivalent branch, checked whether [[[pdlf:app-factory/phase-b-discover-and-define/b16-reference|/domain-modeling]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-reference.md)'s own behavior already
covers the need: it does. "Cross-reference with code" — check whether the
code agrees with what's stated, surface contradictions — fires automatically
whenever code exists to check against. New-project entry has no code yet at
Step 16; the discipline is simply idle, no harm. Existing-project entry has
code, so it fires and does the reconciliation work the old draft's separate
mode was reaching for. One procedure, context differs by entry mode — same
principle already governing every other step.

## Correction 3 — file placement doesn't match Matt's default

Matt's skill defaults to `CONTEXT.md` + `docs/adr/000N-{slug}.md` at repo
root. PDLF already has an established ADR convention (`adr-local/`, paired
with `adr-global/`) predating this research. Resolved by explicit override
at invocation, same technique used for Step 14 overriding
[[[pdlf:app-factory/phase-b-discover-and-define/b14-reference|/plan-ceo-review]]](C:/pdlf/app-factory/phase-b-discover-and-define/b14-reference.md)'s design-doc auto-detection: state the destination paths
in the prompt rather than accepting the skill's default. Kept Matt's
numbering+slug filename convention; changed only the parent folder.

## Why included at all — addressed directly, not assumed

Developer asked directly whether this step earns its place before agreeing
to proceed. Answer given and accepted: PDLF's premise is a non-technical
developer running a multi-session pipeline with an agent that has no native
memory. GBrain solves that for facts; `CONTEXT.md` solves the same problem
for vocabulary. Without it, a term can drift meaning across sessions with no
one positioned to catch it before Phase C builds on top of the drift.

## Prerequisite confirmed via Step 11

Whether Matt Pocock skill setup (`setup-matt-pocock-skills`) happens for a
project PDLF builds, not just for `dev-makepdlf` itself, was open going into this
step. Step 11 item 16 confirms it does: "Set up system files... Set up Matt
Pocock skills configuration" runs for every project at init, both entry
modes. No separate check needed in Step 16 itself.

## Learnings

- Same lesson as Steps 14/15: a skill's name and its README blurb aren't
  enough — [[[pdlf:app-factory/phase-b-discover-and-define/b16-reference|/domain-modeling]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-reference.md) reads like a standalone workflow from its
  one-line description everywhere except its own `SKILL.md` body. Only
  reading the actual file caught this.
- Matt Pocock's skill ecosystem is structured differently from GStack's:
  small, single-purpose files that compose (`/grilling` + [[[pdlf:app-factory/phase-b-discover-and-define/b16-reference|/domain-modeling]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-reference.md)
  = `/grill-with-docs`) rather than large self-contained skills with their
  own preambles and telemetry. Worth expecting this pattern again for Steps
  19, 37, 38, 39, 40 (the other Matt Pocock steps) — check whether each of
  those is actually invoking a composed skill correctly before assuming the
  old drafts got it right.

## Open, not yet decided

- Whether Steps 19/37/38/39/40's Matt Pocock invocations have the same
  "wrong skill name" risk as this step did. Not checked yet — carry into
  each of those steps' own rebuild.
- `docs/agents/issue-tracker.md`-style config path (from
  `setup-matt-pocock-skills`) for the MB5PDLF project specifically — Step 11
  confirms the setup runs but doesn't spell out the resulting file paths.
  Not load-bearing for Step 16 itself; relevant when Step 19 ([[[pdlf:app-factory/phase-c-design-and-plan/c19-reference|Step 19 to Tickets]]](C:/pdlf/app-factory/phase-c-design-and-plan/c19-reference.md))
  is rebuilt.

## Global conventions applied throughout

- No `<project-library>` placeholder — `dev-{slug}\{slug}-project-library`
  in prose, full absolute path in any literal command
- The agent never commits or pushes. Every step ends by explaining what was done, stopping and asking David to run `/mb-close-out`.
- No Step 3 / disposition-table / the retired `sop-existing-project-resume-audit.md`
  references anywhere in this file
- Naming follows [[[default:specifications-global/spec-nomenclature|Spec: Nomenclature]]](C:/dev/project-library-global/specifications-global/spec-nomenclature.md)'s Stepwise File Naming table

## Later decisions

1. **`mb-sentinel-review` invoked at item 7, 2026-08-27.** Step 16 matches
   the retired `sentinel-security-system-plan.md` Section 9's own table exactly — "Domain model,"
   Low/Medium scrutiny, "sensitive data or security-relevant entities being created?"
   Placed after `CONTEXT.md` is updated (item 5) and ADRs are offered (item 6), before
   the gate — a real `FLAG` or `ESCALATE` finding is part of what the developer
   approves at `domain-locked`, not something surfaced only afterward. `mb-sentinel-review`
   itself never implements a fix; it stops and reports, per its own hard rules.
   Renumbered items 7 through 14 to 8 through 15 to accommodate this insertion; one
   stale cross-reference ("asked at item 13") corrected to item 14 in the Reference
   section as a result.
2. **Two real gaps found and closed, 2026-08-27.** First: a CLEAR outcome from
   `mb-sentinel-review` left no durable record — nothing to prove the review ever ran,
   once the conversation ended. Fixed: `triage_label` gained a sixth allowed value,
   `'clear'`, via a real migration, and the skill now writes a resolved row on CLEAR,
   the same as it already did for FLAG and ESCALATE. Second: nothing verified item 7's
   instruction to invoke `mb-sentinel-review` was actually followed, rather than
   silently skipped — a written instruction alone was never a guarantee, the same
   principle already applied everywhere else in this document set. Fixed: new item 9
   requires a real `triage_findings` row to exist for this step's `step_id` before the
   gate procedure may begin — no row, no gate, a deviation request instead. Items 9
   through 15 renumbered from the prior 8 through 14 as a result; one further stale
   cross-reference ("asked at item 14") corrected to item 15.

## From `pdlf-build-plan.md`: step entry

### Phase B — Discover and Define

Ends with the gate `domain-locked` (Step 16).

#### Step 16: Domain modeling

**Must achieve:** the application's vocabulary fixed, so that a term means the same thing in every later step, and the decisions that are hard to reverse recorded, before Phase C builds on them.

**Starts from:** Step 15's plan and test plan; for an existing application, its existing `CONTEXT.md`, decision records and code, marked as prior material.

**Produces:** `docs-local\CONTEXT.md` (the glossary) and any decision records in `adr-local\`, in the documentation repository.

**Carried out by:** Matt Pocock `/grill-with-docs`, which runs a `/grilling` interview using `/domain-modeling`.

**Must be built so that:**
- the skill is told the project's own file locations, in place of its defaults;
- the interview runs as the skill is designed: each round asks every question that can be asked at that point, each with a recommended answer, and waits for the developer; PDLF never limits or reshapes the skill's questions; each settled term is written to `CONTEXT.md` at once, as a glossary only, with no implementation detail;
- a decision record is offered only for a decision that is hard to reverse, surprising without context and the result of a real trade-off;
- for an existing application, what the documents say is checked against the code, and contradictions are shown to the developer;
- Anvil's `data-models` skill is read and used to check that the vocabulary and the data design agree: every entity named in `CONTEXT.md` has a clear owner and place in the data design, and the data design uses only the vocabulary's terms;
- the security review `mb-sentinel-review` checks for sensitive data or security-relevant entities before the gate; a finding stops the step and goes to the developer; the review's record in the ledger is checked, so that its run is proven, not assumed.

**BFT level:** Full (gate).

**Gate:** `domain-locked`: the vocabulary and decisions are locked; no new terms without reopening the gate.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `grill-with-docs`, `grilling`, `domain-modeling` (Matt Pocock) → `CONTEXT.md` and the ADRs, then every later step.
- `data-models` (Anvil): checks that the vocabulary and the data design agree → Step 17's tables.
- `graphify`: for an existing application, checks what the documents say against the code → the contradictions shown to the developer.
- `prototype` (Matt Pocock), only when an entity's life cycle is uncertain → `CONTEXT.md` and the ADRs.
- `mb-archify-scope`, then `archify`: the domain map (entities and their relationships) → the developer at the gate, then Step 17.
- `mb-sentinel-review`, Low/Medium → `triage_findings`.

**Testing:** every entity in `CONTEXT.md` has an owner and a place in the data design. **Vocabulary home:** `CONTEXT.md` holds the terms of this application only; terms common to every application, every system and PDLF are in [[[default:specifications-global/spec-nomenclature|Spec: Nomenclature]]](C:/dev/project-library-global/specifications-global/spec-nomenclature.md).

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

**1.7 Anvil and our own standards are almost absent from Phase B.** The intent's second success criterion is that Anvil's standards are applied throughout. Phase B locks the architecture (Step 15) and the domain model (Step 16) without once using Anvil's own skills. The catalogue's Anvil skill `data-models` says it should be used "before choosing an architecture for persisted domain data", which is exactly what Steps 15 and 16 do. Likewise, the only use of `project-library-global` is a vague "local/global conflict check"; no step names which standard it applies.

**1.9 One step improvises where a skill exists.** Step 12 tells OpenCode to "query the developer diligently" until the scope is clear. The catalogue has a skill for exactly that, `grilling` (and `grill-me`), which Step 16 already uses. Under the intent's rule that skills take precedence, Step 12 should use it.

## 2. What we could have done better

**2.1 Too many documents per step.** Each step has a step file, build notes and a decision tree, and was also described in `workflow.md` and the step mapping. That is five places for one step, and they drifted apart. The decision trees are hand-written pictures of the step's action list, so they are a second copy of it. One step file, one build-plan entry and one built-report entry are enough.

**2.4 The biggest commitments in Phase B are not gated.** Phase B's only gate is at Step 16. Yet the concept (Step 12) and the scope (Step 14) are the commitments everything else rests on. They are approved inside their steps, but not as gates, and the concept is only locked formally at Step 21.

**2.5 Skill choices were made step by step, not from the catalogue.** Each step picked the skill that came to mind. The catalogue was never read as a whole to ask: which installed skill best serves this step, and which skill is installed but unused?

## 3. How Phase B should be corrected

1. **Bring all five steps into line with the intent's rules:** close-out by `/mb-close-out`, the agent never commits, seven ledger tables, no registry or inventory, artifact copies to `C:\pdlf\output\`, no devlog or judgement trail, skills take precedence.

2. **Remove the repeated rules from the step files.** Each step file states only what is particular to it and points to the rules every step follows.

3. **Give every skill a standard context pack** at invocation: the five-app structure, the no-multi-tenancy decision, the Material 3 design standard, and the `project-library-global` standards the step applies.

4. **Add Anvil's `data-models` skill to Steps 15 and 16,** where the architecture and the domain model are fixed.

9. **Run Phase B on the test application** (the Daily Intentions Tracker in `mb5pdlf`), answer the open questions from the run, and only then record the steps as finished.

10. **Move the lessons out of the build notes** into the build plan's rules, then retire the build notes and decision trees.
