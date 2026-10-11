---
title: "pdlf-build-plan"
doc-id: "mb-64817b10"
updated: "2026-10-11"
---
# PDLF Build Plan

## Preamble

### Purpose

This document is the blueprint for building PDLF. It says what PDLF's steps must achieve, the rules every step is built to, the decisions that span more than one step, and the order in which the steps are built or corrected.

It works with three other things:

- **`pdlf-intent.md`** states what PDLF is meant to be. This build plan turns that intent into steps. Where the two disagree, the intent wins and this plan is corrected.
- **The step files** in `stepwise/` are what is actually built. Each step file holds its own detail: its inputs, outputs, process and action list. Where a step entry below still carries an action list from the old `workflow.md`, that list is checked against the step file and then removed. This build plan does not repeat that detail; it leads, and the step files follow it.
- **`pdlf-built-report.md`** (in `pdlf-library/docs-local/`) records what has been built so far.

This document is about building PDLF, not running it. When PDLF is built, it is retired together with `stepwise/`.

### References that apply to every step

Every step follows [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md), applies [[[pdlf:pdlf-library/specifications-local/spec-bft|Spec: BFT]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md), and names things per [[[default:specifications-global/spec-nomenclature|Spec: Nomenclature]]](C:/dev/project-library-global/specifications-global/spec-nomenclature.md). References that apply to particular steps are named at those steps.

### What this document holds

#### 1. Rules every step follows

Every step is built to these rules, which come from `pdlf-intent.md`. They are stated once here and not repeated at each step.

- **It starts with a GBrain search** of the sources it needs, named explicitly (normally `{slug}`, `{slug}-project-library` and `project-library-global`), and it reads the actual file a search points to before applying it.
- **The developer approves every change.** The step explains each decision in plain language, never jumps a gate, and never passes one without the developer's approval.
- **Skills take precedence.** When a skill in PDLF's library covers a task, the step uses it and does not improvise.
- **Deviations are decided by the developer.** If the step cannot be done as written, it stops, sets out the options and what each costs, and the developer decides. The decision is recorded in the ledger.
- **It leaves its record:** a row in the ledger, its BFT record at its level, and a Step Receipt at `dev-{slug}\{slug}-project-library\pdlf\step-NN-receipt.md`.
- **Every artifact goes to its canonical place,** with a copy in `C:\pdlf\output\` for the developer's convenience.
- **The agent never commits or pushes.** Close-out is `/mb-close-out`, run when the developer asks for it; new knowledge reaches GBrain only through close-out and `mb-submit-memory`.
- **No application is ever multi-tenant.** Every step that shapes data or code keeps each client's application and database separate.

#### 2. The pipeline at a glance

One entry per step, below: what it must achieve, who carries it out, its gate if it has one, whether it runs once per feature, and the references it applies.

#### 3. Decisions that span several steps

The entry points in Steps 2 to 10, where the gates sit and what each approves, the BFT thinking checkpoints, which `project-library-global` standard each step applies, and the steps that build the remaining apps after Step 46. To be written.

#### 4. Build order

Which steps are built or corrected next, and in what sequence. To be written.

---

## The Build Plan

### Before the pipeline

#### Step 1: Orchestrator

**Must achieve:** asks the developer the questions that establish the entry point, selects the steps that entry needs using `orchestrator-run-plan.md`, runs them in order, and stops at every gate for the developer's approval.

**Carried out by:** OpenCode, as the orchestrator. Not yet designed.

#### Steps 2 to 10: Entry points

**Must achieve:** the entry points for a new feature on an existing application, for an update or upgrade, and for returning to one of the other apps of an existing five-app set. Not yet designed.

### Phase A — Discover and Define

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

#### Step 13: Not used

This step number is not used.

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
- Step 12's input notice is carried forward if its design doc was synthesized.

**BFT level:** Full.

**References:** [[[pdlf:pdlf-library/policy-local/pol-step-conditional-state|Step Conditional State Policy]]](C:/pdlf/pdlf-library/policy-local/pol-step-conditional-state.md).

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

#### Step 16: Domain modeling

**Must achieve:** the application's vocabulary fixed, so that a term means the same thing in every later step, and the decisions that are hard to reverse recorded, before Phase B builds on them.

**Starts from:** Step 15's plan and test plan; for an existing application, its existing `CONTEXT.md`, decision records and code, marked as prior material.

**Produces:** `CONTEXT.md` (the glossary) and any decision records in `adr-local\`, in the documentation repository.

**Carried out by:** Matt Pocock `/grill-with-docs`, which runs a `/grilling` interview using `/domain-modeling`.

**Must be built so that:**
- the skill is told the project's own file locations, in place of its defaults;
- the interview settles one decision at a time, gives a recommended answer and waits for the developer; each settled term is written to `CONTEXT.md` at once, as a glossary only, with no implementation detail;
- a decision record is offered only for a decision that is hard to reverse, surprising without context and the result of a real trade-off;
- for an existing application, what the documents say is checked against the code, and contradictions are shown to the developer;
- the security review `mb-sentinel-review` checks for sensitive data or security-relevant entities before the gate; a finding stops the step and goes to the developer; the review's record in the ledger is checked, so that its run is proven, not assumed.

**BFT level:** Full (gate).

**Gate:** `domain-locked`: the vocabulary and decisions are locked; no new terms without reopening the gate.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

### Phase B — Design and Plan

Ends with the gates `concept-locked` (Step 21) and `wireframes-approved` (Step 26).

#### Step 17: Create Anvil data tables

**Must achieve:** The data tables are built in Anvil from the domain model and the ADRs.

**Carried out by:** The developer, by hand in the Anvil editor.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to schema construction
2. Developer: Build data tables/schema in Anvil IDE — Per ADRs and authoritative schema from Steps 15–16
3. Verify tables exist — STOP if missing
4. Write Step 17 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-17-receipt.md`
6. Apply BFT — Light level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 18: Pull to local

**Must achieve:** The code repository is pulled to local after the tables are built.

**Carried out by:** The developer, by hand.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to codebase state
2. Pull Anvil-connected code repo to local — Updated schema from Step 17
3. Verify local repo updated — STOP if schema not present
4. Write Step 18 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-18-receipt.md`
6. Apply BFT — None
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 19: To tickets

**Must achieve:** Breaks the plan into features (tickets) in the order they depend on each other. This is the feature list the build loop works through.

**Carried out by:** Matt Pocock, using `to-tickets`.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to issue decomposition
3. Read Step 14 CEO plan — `<project-library>/gstack-outputs/step-14-ceo-plan.md` (refined by Step 15)
4. Read CONTEXT.md + ADRs from Step 16
5. Confirm issue tracker config — From `/setup-matt-pocock-skills`
6. Invoke Matt `to-tickets` — Breaks spec into tracer-bullet issues in dependency order
7. Verify outputs — Issues published to project issue tracker; STOP if missing
8. Write Step 19 ledger row — `completed_at`
9. Generate Step Receipt — `<project-library>/pdlf/outputs/step-19-receipt.md`
10. Apply BFT — Full level
11. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 20: Design consultation

**Must achieve:** Builds the application's design system (`DESIGN.md`) on Material 3 and David's design standards. In a test run, the developer may abbreviate or skip it.

**Carried out by:** GStack, using `/design-consultation`.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to design system
2. Check test-mode flag — Present abbreviation offer (full/abbreviate/skip) if in test mode
3. Invoke GStack `/design-consultation` — Researches landscape, builds DESIGN.md + preview page
4. Verify outputs — DESIGN.md written, font/color preview page, design tokens; STOP if missing
5. Write Step 20 ledger row — `completed_at`
6. Generate Step Receipt — `<project-library>/pdlf/outputs/step-20-receipt.md`
7. Apply BFT — Full level
8. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 21: Concept sanity audit

**Must achieve:** Cross-checks everything produced so far for contradictions and reports the verdict.

**Carried out by:** OpenCode.

**Gate:** `concept-locked`: the concept is locked; no new feature without reopening the gate.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to cross-artifact consistency
2. Read all Phase A+B outputs — CEO review (Step 14), Eng review (Step 15), CONTEXT.md + ADRs (Step 16), DESIGN.md (Step 20)
3. Cross-reference each document pair for contradictions
4. Produce audit report — What was checked, findings, discrepancies, verdict
5. Save audit report — `<project-library>/pdlf/step-21-concept-audit.md`
6. Execute gate procedure — per `specifications-local/spec-gate-procedure.md`
7. Gate: `concept-locked` — Full BFT, gate summary, developer approval required; no new feature without formal gate reopening
8. Write Step 21 ledger row — `completed_at`
9. Generate Step Receipt — `<project-library>/pdlf/outputs/step-21-receipt.md`
10. Apply BFT — Full (gate override)
11. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 22: Wireframes, phase 1

**Must achieve:** Produces the structural wireframes, in black and white.

**Carried out by:** The Magdoub wireframe skill.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to wireframe generation
2. Invoke Claude Wireframe Skill (Magdoub) — Phase 1: 5 B&W UX wireframe approaches
3. Verify outputs — `wireframe/brain/design-context.md`, `design-taste.md`, `wireframe/DDMM-{feature}/index.html` + `styles.css`; STOP if missing
4. Write Step 22 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-22-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 23: Plan design review

**Must achieve:** Rates the design for usability and identifies gaps.

**Carried out by:** GStack, using `/plan-design-review`.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to design review
2. Invoke GStack `/plan-design-review` — Rates UX dimensions 0–10, identifies gaps
3. Verify outputs — GSTACK REVIEW REPORT appended to plan file; STOP if missing
4. Write Step 23 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-23-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 24: Plan developer-experience review

**Must achieve:** Reviews developer-experience friction in the plan.

**Carried out by:** GStack, using `/plan-devex-review`.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to developer experience review
2. Invoke GStack `/plan-devex-review` — Reviews API/CLI/SDK friction points and onboarding time
3. Verify outputs — DX scorecard appended to plan file; STOP if missing
4. Write Step 24 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-24-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 25: Not used

This step number is not used.

#### Step 26: Wireframes, phase 2

**Must achieve:** Produces the polished wireframes.

**Carried out by:** The Magdoub wireframe skill.

**Gate:** `wireframes-approved`: the wireframes are approved and Phase B ends.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to wireframe refinement
2. Invoke Claude Wireframe Skill (Magdoub) — Phase 2: Clean + Polished color variants
3. Verify outputs — `styles-opt1.css` through `styles-opt5.css`; STOP if missing
4. Execute gate procedure — per `specifications-local/spec-gate-procedure.md`
5. Gate: `wireframes-approved` — Full BFT, gate summary, developer approval required to proceed beyond Phase B
6. Write Step 26 ledger row — `completed_at`
7. Generate Step Receipt — `<project-library>/pdlf/outputs/step-26-receipt.md`
8. Apply BFT — Full (gate override)
9. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 27: Screen production

**Must achieve:** Produces screens from the approved wireframes. Deferred: runs only if the developer asks for it.

**Carried out by:** OpenCode.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to screen production
2. Check deferral status — Skip unless explicitly requested by developer
3. If active: Produce screen HTML from approved wireframe (Step 26)
4. Apply wireframe fidelity checklist
5. Apply screen standard compliance checklist
6. Verify outputs — Screen HTML, both checklists; STOP if missing
7. Write Step 27 ledger row — `completed_at` (or `deferred`)
8. Generate Step Receipt — `<project-library>/pdlf/outputs/step-27-receipt.md`
9. Apply BFT — Full level (if active)
10. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 28: Screen to PNG

**Must achieve:** Converts the screens to images. Deferred: runs only if the developer asks for it.

**Carried out by:** An external tool.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to screen conversion
2. Check deferral status — Skip unless explicitly requested by developer
3. If active: Convert screen HTML from Step 27 to PNG via external rendering tool
4. Verify output — Screen PNG in same folder as Step 27; STOP if missing
5. Write Step 28 ledger row — `completed_at` (or `deferred`)
6. Generate Step Receipt — `<project-library>/pdlf/outputs/step-28-receipt.md`
7. Apply BFT — None
8. Follow execution sequence — Housekeeping, stop, wait for continue

### Phase C — Scaffold and Assemble

Ends with the gate `architecture-verified` (Step 34).

#### Step 29: Build UI forms

**Must achieve:** The forms are built in Anvil from the approved wireframes.

**Carried out by:** The developer with Anvil's AI, by hand in the Anvil editor.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to UI form construction
2. Developer + Anvil AI: Build UI forms in Anvil IDE — From approved wireframes and screens
3. Verify forms exist in Anvil IDE — STOP if missing
4. Write Step 29 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-29-receipt.md`
6. Apply BFT — Light level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 30: Pull to local

**Must achieve:** The code repository is pulled to local after the forms are built.

**Carried out by:** The developer, by hand.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to codebase state
2. Pull Anvil-connected code repo to local — Component tree with Anvil AI's wiring
3. Verify local repo updated — STOP if UI forms not present
4. Write Step 30 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-30-receipt.md`
6. Apply BFT — None
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 31: Scaffold planning

**Must achieve:** Plans the modules and functions the code needs, as empty stubs, in `scaffold-plan.md`.

**Carried out by:** OpenCode.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to module/function structure planning
2. Review Step 15/16 architecture and domain model — TDD cluster, CONTEXT.md, ADRs
3. Review Step 30 pulled UI form structure
4. Review Step 21 concept audit report
5. Plan module/function structure — Determine what stubs to create
6. Write `scaffold-plan.md` — Saved to `<project-library>/`
7. Verify output — `scaffold-plan.md` exists; STOP if missing
8. Write Step 31 ledger row — `completed_at`
9. Generate Step Receipt — `<project-library>/pdlf/outputs/step-31-receipt.md`
10. Apply BFT — Full level
11. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 32: Physical scaffold build

**Must achieve:** The empty modules and functions are created in Anvil from the scaffold plan.

**Carried out by:** The developer, by hand in the Anvil editor.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to scaffold construction
2. Developer: Create empty client-code modules and server modules/functions in Anvil IDE — Per `scaffold-plan.md`
3. Verify stubs exist in Anvil IDE — STOP if missing
4. Write Step 32 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-32-receipt.md`
6. Apply BFT — Light level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 33: Pull to local

**Must achieve:** The code repository is pulled to local after the scaffold is built.

**Carried out by:** The developer, by hand.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to codebase state
2. Pull Anvil-connected code repo to local — Scaffold structure
3. Verify local repo updated — STOP if stubs not present
4. Write Step 33 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-33-receipt.md`
6. Apply BFT — None
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 34: Architectural sanity audit

**Must achieve:** Checks the tables, forms and scaffold against the locked decisions, so that nothing has drifted before any code is written.

**Carried out by:** OpenCode.

**Gate:** `architecture-verified`: the structure is verified and coding may begin.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to architecture verification
2. Compare actual Anvil data tables against ADRs and domain model — Every table/column traces to a locked decision
3. Compare actual UI forms against approved screens and DESIGN.md
4. Compare actual scaffolding against `scaffold-plan.md` — Every planned module/function exists, nothing improvised
5. Check for drift — If found, correct Anvil-side artifact or formally update plan/ADR per deviation mechanism
6. Produce audit report — What was checked, findings, discrepancies, verdict
7. Save audit report — `<project-library>/pdlf/step-34-architecture-audit.md`
8. Execute gate procedure — per `specifications-local/spec-gate-procedure.md`
9. Gate: `architecture-verified` — Full BFT, gate summary, developer approval required before any code-writing begins
10. Write Step 34 ledger row — `completed_at`
11. Generate Step Receipt — `<project-library>/pdlf/outputs/step-34-receipt.md`
12. Apply BFT — Full (gate override)
13. Follow execution sequence — Housekeeping, stop, wait for continue

### Phase D — Build and Verify

Steps 35 to 40B run once per feature, one feature at a time; the run plan governs the loop. Each feature ends with the gate `build-verified` (Step 39).

#### Step 35: Build

**Must achieve:** Builds one feature, tested at three levels: its logic alone, connected to the live Anvil app (with a backup before and after), and by hand in the browser. The developer signs the feature off.

**Carried out by:** OpenCode.

**Runs:** once per feature.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to this feature
2. Write the pure-logic function
3. Write Level 1 tests and run them locally
4. Decision point: Level 1 pass? Continue. Fail? Fix and retry
5. Create pre-integration backup
6. Write server-module (integration) wrapper
7. Write Level 2 tests
8. Push to Anvil — `git push` to branch, no auto-publish
9. Run Level 2 tests via Uplink against Development Environment
10. Decision point: Level 2 pass? Create post-success backup and continue. Fail? Restore from pre-integration backup, fix, retry
11. Pull repo back to local
12. Level 3: Manual/browser verification of complete feature
13. Decision point: Developer signoff on this feature
14. Generate Step Receipt for 35.N — `<project-library>/pdlf/outputs/step-35-{N}-receipt.md`
15. This feature is complete; the next feature starts again at Step 35 (the run plan governs the loop)
16. Follow execution sequence — Per cycle
17. Apply BFT — Full (per feature)

#### Step 35A: Testing

**Must achieve:** Broader testing of the feature, and a security check of the development and test tools (`pip-audit`).

**Carried out by:** OpenCode.

**Runs:** once per feature.

#### Step 36: Design review

**Must achieve:** A visual audit of the feature as it will ship, after any fixes from Step 40B.

**Carried out by:** GStack, using `/design-review`.

**Runs:** once per feature.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to visual audit
2. Invoke GStack `/design-review` — 80-item live-site visual audit; before/after screenshots, atomic fix commits
3. Verify outputs — Design audit report, screenshots, fix commits; STOP if missing
4. Write Step 36 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-36-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 37: Code review

**Must achieve:** Reviews the feature's code for bugs that would break in use. Findings are written to `step-37-findings.md`, including a clean-pass statement.

**Carried out by:** GStack, using `/review`.

**Runs:** once per feature.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to pre-landing code review
2. Invoke GStack `/review` — Finds bugs that pass CI but would break in production; auto-fixes obvious ones
3. Verify outputs — Review report, AUTO-FIXED commits; STOP if missing
4. Write Step 37 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-37-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 38: Quality testing

**Must achieve:** Tests the feature, and checks that earlier features still work. Findings are written to `step-38-findings.md`, including a clean-pass statement.

**Carried out by:** GStack, using `/qa`.

**Runs:** once per feature.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to QA testing
2. Invoke GStack `/qa` — Systematic QA testing; bug fixing; generates regression tests
3. Verify outputs — QA report with before/after screenshots, fix commits, regression test files; STOP if missing
4. Write Step 38 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-38-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 38A: Dependency check

**Must achieve:** Captures Anvil's own security check of the server packages, when the server environment was rebuilt.

**Carried out by:** OpenCode.

**Runs:** once per feature.

#### Step 39: Triage

**Must achieve:** Sorts the findings of Steps 37 and 38 for this feature.

**Carried out by:** Matt Pocock, using `triage`.

**Runs:** once per feature.

**Gate:** `build-verified`, for this feature: it is signed off and the next feature may start. Step 41 cannot begin until every feature has passed.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to issue triage
2. Invoke Matt `triage` — Updates issue tracker: comments, labels, state changes, agent briefs
3. Verify outputs — Labels applied, comments added, briefs written; STOP if missing
4. Write Step 39 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-39-receipt.md`
6. Apply BFT — Light level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 40: Architecture scan

**Must achieve:** An optional, read-only scan of the feature's code architecture. The developer decides for each feature whether it runs.

**Carried out by:** Matt Pocock, using `improve-codebase-architecture`.

**Runs:** once per feature.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to architecture health scan
2. Present RUN/SKIP recommendation with justification
   - Branch RUN: Invoke Matt `improve-codebase-architecture` — Interactive HTML architecture report
   - Branch SKIP: Skip the scan
3. Write Step 40 ledger row — `completed_at`
4. Generate Step Receipt — `<project-library>/pdlf/outputs/step-40-receipt.md`
5. Apply BFT — Full
6. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 40B: Approved fixes

**Must achieve:** Applies only the fixes the developer approved from Step 40. Skipped if Step 40 did not run or found nothing to fix.

**Carried out by:** OpenCode.

**Runs:** once per feature.

### Phase E — Ship and Monitor

Ends with the gates `production-released` (Step 44) and `released` (Step 46). Steps 42 to 44 still describe a staging and production split that PDLF does not have; they are rebuilt around the `develop` → `stable` release.

#### Step 41: Ship

**Must achieve:** Tests, versions and records the release, and pushes it; it stops at the push.

**Carried out by:** GStack, using `/ship`.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to ship readiness
2. Invoke GStack `/ship` — Tests, VERSION bump, CHANGELOG, commit, push; stops at push
3. Verify outputs — Merged base branch, tests pass, VERSION bumped, CHANGELOG updated, branch pushed; STOP if missing
4. Write Step 41 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-41-receipt.md`
6. Apply BFT — Light level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 42: Publish to staging

**Must achieve:** Still describes publishing to a staging environment, which PDLF does not have. To be rebuilt.

**Carried out by:** The developer, by hand.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to staging deployment
2. Developer: Publish the pushed commit to Staging environment in Anvil IDE — Production untouched
3. Verify output — App running at Staging URL; STOP if not reachable
4. Write Step 42 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-42-receipt.md`
6. Apply BFT — None
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 42A: Staging integration tests

**Must achieve:** Still describes a full integration test run on staging. To be rebuilt.

**Carried out by:** GStack and OpenCode.

#### Step 43: Staging smoke test

**Must achieve:** Still describes a smoke test on staging. To be rebuilt.

**Carried out by:** GStack, using `/qa` or `/canary`.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to staging verification
2. Invoke GStack `/qa` or `/canary` — Retargeted at Staging URL from Step 42
3. Verify output — Smoke test report: pass/fail at Staging; STOP if failing
4. Write Step 43 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-43-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 44: Release

**Must achieve:** Still describes promoting staging to production; to be rebuilt as the `develop` → `stable` release to `master_template`, which the developer performs.

**Carried out by:** The developer, by hand.

**Gate:** `production-released`: the application is released.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to production deployment
2. Developer: Promote the same reviewed commit from Staging to Production in Anvil IDE — Rollback is re-pointing, not `git revert`
3. Execute gate procedure — per `specifications-local/spec-gate-procedure.md`
4. Gate: `production-released` — Full BFT, gate summary, developer approval required; app is now live
5. Write Step 44 ledger row — `completed_at`
6. Generate Step Receipt — `<project-library>/pdlf/outputs/step-44-receipt.md`
7. Apply BFT — Full (gate override)
8. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 45: Production check

**Must achieve:** Watches the released application for errors and performance problems.

**Carried out by:** GStack, using `/canary`.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to post-deploy monitoring
2. Invoke GStack `/canary` — Targeted at Production URL from Step 44; watches for console errors, performance regressions
3. Verify output — Canary report with initial health check; STOP if critical failures
4. Write Step 45 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-45-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 46: Learning

**Must achieve:** The retrospective: what this build taught is captured and written into the sources the next build reads.

**Carried out by:** OpenCode.

**Gate:** `released`: the build cycle closes.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to retrospective and learning
2. Invoke GStack `/retro` — Retrospective report
3. Invoke GStack `/learn` — Capture learnings
4. Invoke GStack `/context-save` — Persist working state
5. Update ISA — Fill Verification section, update Changelog
6. Update registry — `current_step: 46`, `last_gate: "released"`, `active: false`
7. Sync and embed GBrain — Learnings now searchable for next project
8. Execute gate procedure — per `specifications-local/spec-gate-procedure.md`
9. Gate: `released` (jointly with Step 45) — Full BFT, gate summary, developer approval required to close the project cycle
10. Write Step 46 ledger row — `completed_at`
11. Generate Step Receipt — `<project-library>/pdlf/outputs/step-46-receipt.md`
12. Apply BFT — Full (gate override)
13. Follow execution sequence — Housekeeping, stop

### After Step 46: the remaining apps

**Must achieve:** the steps that build the rest of the five-app set in the same pipeline: `blank_client_template`, the first client instance with the provisioning procedure and the README every instance carries, and the management tooling. Not yet designed.
