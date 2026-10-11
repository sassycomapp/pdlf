---
title: "pdlf-phase-b-review"
doc-id: "mb-9f7e7001"
updated: "2026-10-11"
---
# PDLF Phase B Review

## Purpose

This document reviews Phase B of PDLF (Steps 11, 12, 14, 15 and 16) as a case study, before Phases C to F are built. It looks at what was done wrong, what could have been done better, how Phase B should be corrected, and how the method should change for Phase C. It judges Phase B against `pdlf-intent.md`, against the principles of mybizz-os, and against the skills catalogue. It is not a plan for Phase C.

The evidence is the five step files, their build notes and decision trees, the build plan, the built report, the old `workflow.md`, the old step mapping, and `skills-catalog.md`.

---

## 1. What we did wrong

**1.1 We built the steps before we had stated the intent.** The order was step file first, build notes second and intent last. Every step therefore carries assumptions that the intent later reversed: housekeeping questions at the end of every step, a ledger with six tables, a project registry and a project inventory that no longer exist, makePDLF paths and prefixes, the devlog and judgement trail, and the old rule "use a skill only when it beats OpenCode". None of these were careless; they were right when written and became wrong when the intent was settled. The cost is that all five steps now need repair before they can be packaged.

**1.2 We called the steps "built" without ever running them.** Not one of the five steps has been run against a real application. Several open questions can only be answered by a run: whether `/plan-eng-review` finds "the active plan file" inside OpenCode, where `TODOS.md` belongs, and whether the statement that "a design doc already exists" really stops GStack from re-offering `/office-hours`. mybizz-os's own principle is "present is not working, and completed is not worked". By that principle, Phase B is designed, not built.

**1.3 Each step repeats the rules that apply to every step.** Every step file spells out, in its own words, the GBrain search, the ledger row, the Step Receipt, the BFT, the two housekeeping questions and a five-action memory sequence. The same rule is written five times, slightly differently each time, so one change (such as moving close-out to `/mb-close-out`) has to be made in five places and is easily missed in one. This breaks "one fact, one home".

**1.4 Each step ran its own memory and dream cycle.** The housekeeping asked, at every step, to run `gbrain dream` and `gbrain eval suspected-contradictions`. In mybizz-os, the dream cycle is a long, heavy process run on Sundays after the diagnostic, with a manual review afterwards. Running it after every step would have cost hours across a build and buried the developer in reviews. The intent's close-out rule replaces this.

**1.5 We wrapped outside skills without first reading them.** Three steps were designed from a skill's name or summary and were wrong: Step 15 assumed five architecture documents that the skill never produces; Step 16 invoked `/domain-modeling`, which cannot run on its own; and Step 14 used the wrong GStack save path. Each mistake was caught later, by reading the skill's source, and written down as a lesson in the build notes, three times over. The lesson was never turned into a rule before the next step was designed.

**1.6 Lessons went into build notes, where nobody reads them.** Each step's build notes end with "Learnings". The intent says a lesson is written into the source that the next build reads. The build notes are not that source: they are history. The lessons from Phase B ("read the skill's source first", "paste context into the skill, because it does not read our folders", "state file destinations explicitly") belong in the build plan's rules.

**1.7 Anvil and our own standards are almost absent from Phase B.** The intent's second success criterion is that Anvil's standards are applied throughout. Phase B locks the architecture (Step 15) and the domain model (Step 16) without once using Anvil's own skills. The catalogue's Anvil skill `data-models` says it should be used "before choosing an architecture for persisted domain data", which is exactly what Steps 15 and 16 do. Likewise, the only use of `project-library-global` is a vague "local/global conflict check"; no step names which standard it applies.

**1.8 The non-negotiable rules are not given to the skills.** The intent says AI agents are given the no-multi-tenancy rule as context before any code is generated, because they reach for shared databases by default. Steps 12, 14 and 15 shape the architecture through generic GStack skills, and none of them is given the five-app structure, the no-multi-tenancy decision or the Material 3 design standard. A generic architecture review is exactly where a shared-database design would be proposed.

**1.9 One step improvises where a skill exists.** Step 12 tells OpenCode to "query the developer diligently" until the scope is clear. The catalogue has a skill for exactly that, `grilling` (and `grill-me`), which Step 16 already uses. Under the intent's rule that skills take precedence, Step 12 should use it.

---

## 2. What we could have done better

**2.1 Too many documents per step.** Each step has a step file, build notes and a decision tree, and was also described in `workflow.md` and the step mapping. That is five places for one step, and they drifted apart. The decision trees are hand-written pictures of the step's action list, so they are a second copy of it. One step file, one build-plan entry and one built-report entry are enough.

**2.2 The reviews overlap, and every overlap costs the developer questions.** Step 14's CEO review has eleven sections, including architecture, security, data flow, tests and performance. Step 15's engineering review covers architecture, code quality, tests and performance again. Both put every finding to the developer as a separate question. That is the right discipline, but asked twice about the same subjects, the developer faces a very long run of questions, and a tired reviewer is the rubber-stamp that BFT exists to prevent. Each review should have its own remit, so that no subject is reviewed twice.

**2.3 Generic review content does not fit Anvil.** The GStack reviews were written for general web development. Parts of them have no meaning for an Anvil application: build and publish pipelines, worktree parallelisation, N+1 query patterns written for other frameworks. Without Anvil context, the reviews ask about things that do not apply and miss things that do.

**2.4 The biggest commitments in Phase B are not gated.** Phase B's only gate is at Step 16. Yet the concept (Step 12) and the scope (Step 14) are the commitments everything else rests on. They are approved inside their steps, but not as gates, and the concept is only locked formally at Step 21.

**2.5 Skill choices were made step by step, not from the catalogue.** Each step picked the skill that came to mind. The catalogue was never read as a whole to ask: which installed skill best serves this step, and which skill is installed but unused?

---

## 3. How Phase B should be corrected

1. **Bring all five steps into line with the intent's rules:** close-out by `/mb-close-out`, the agent never commits, seven ledger tables, no registry or inventory, artifact copies to `C:\pdlf\output\`, no devlog or judgement trail, skills take precedence.
2. **Remove the repeated rules from the step files.** Each step file states only what is particular to it and points to the rules every step follows.
3. **Give every skill a standard context pack** at invocation: the five-app structure, the no-multi-tenancy decision, the Material 3 design standard, and the `project-library-global` standards the step applies.
4. **Add Anvil's `data-models` skill to Steps 15 and 16,** where the architecture and the domain model are fixed.
5. **Add `secure-software-engineering` to Steps 14 and 15,** where security requirements and the threat model belong. That skill is for prevention during requirements and design, which is earlier than Sentinel's review at Step 16.
6. **Use `grilling` in Step 12** for questioning the developer, in place of the improvised interview.
7. **Give Steps 14 and 15 separate remits:** Step 14 settles scope and ambition; Step 15 settles architecture, tests and performance. Neither reviews the other's subjects.
8. **Decide whether the concept needs its own gate** at the end of Step 12.
9. **Run Phase B on the test application** (the Daily Intentions Tracker in `mb5pdlf`), answer the open questions from the run, and only then record the steps as finished.
10. **Move the lessons out of the build notes** into the build plan's rules, then retire the build notes and decision trees.

---

## 4. How to change our approach for Phase C

**4.1 Intent first, then the plan, then the step.** For each step, write its build-plan entry first (what it must achieve, what it starts from, what it produces, who carries it out, what it must be built so that), and have the developer approve the entry before the step file is touched. The step file is then written to the entry, never the other way round.

**4.2 Choose skills from the catalogue, deliberately.** For each step, read the catalogue and name the skill that best serves it, with the reason. Read that skill's own source before designing around it, and record what it really does in the build-plan entry. Phase C has clear candidates that were not used in Phase B: Anvil's `data-models`, `anvil-yaml` and `client-forms` for the tables and forms; `wizard`, which walks a person through steps only they can perform, for the manual steps in the Anvil editor (Steps 17, 29 and 32); and `writing-for-agents` whenever a step file is written, because step files are instructions for an agent.

**4.3 Anvil and our standards in every step.** Every build-plan entry names the `project-library-global` standard and the Anvil skill it applies. This is the table "which standard each step applies", built step by step instead of afterwards.

**4.4 One home for every rule.** Rules that apply to every step live once in the build plan. A step file holds only what is particular to that step. No step repeats a shared rule in its own words.

**4.5 One step file, nothing beside it.** No new build notes and no hand-drawn decision trees. If a picture is needed, it is generated from the step file, so that it cannot drift.

**4.6 A lesson goes straight into its source.** When building a step teaches something, the lesson is written at once into the build plan's rules, the specification it concerns, or `project-library-global`, never only into a log.

**4.7 Fit for purpose before thoroughness.** For each step, ask whether it earns its place. Phase C has three near-identical "pull to local" steps (18, 30 and 33): one shared procedure may serve all three. For each review, ask what only it covers, so that the developer is never asked the same question twice.

**4.8 Proven before finished.** A step is recorded as built when its step file is complete, and as finished only after it has run on the test application and been packaged as its module. Phase C is run on the test application as soon as its steps are written, not after the whole pipeline exists.
