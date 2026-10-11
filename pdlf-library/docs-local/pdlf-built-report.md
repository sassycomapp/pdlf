---
title: "pdlf-built-report"
doc-id: "mb-36208a1a"
updated: "2026-10-11"
---
# PDLF Built Report

## Preamble

This document records what has been built of PDLF so far, step by step. It states facts only: for each step, its files and whether it has been built; and, once it is built, what it does, what it produces and what was decided while building it. What each step must achieve is in `pdlf-build-plan.md` (in `stepwise/`); this report never repeats it.

The steps are listed in the same order and under the same phases as the build plan, so the two can be read side by side. Every step has an entry, whether or not any work has been done on it yet, so that each piece of work is recorded in its place as it happens.

Each entry is updated whenever its step is built, corrected or packaged. A step is recorded as built when its step file is complete. It is finished when it has also been packaged as its module in `app-factory/`. Steps 11, 12, 14, 15 and 16 are built; no module has been packaged yet.

This report is kept after PDLF is built, as the record of what PDLF consists of.

## The Built Report

### Before the pipeline

#### Step 1: Orchestrator

**File:** `stepwise/step-01-orchestrator.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet designed.

#### Steps 2 to 10: Entry points

**File:** none.

**Status:** Not yet designed.

### Phase A — Discover and Define

#### Step 11: Init

**Status:** Built. Last changed 2026-08-25.

**Files:** `stepwise/step-11-init.md` (the step), `stepwise/step-11-build-notes.md`, `stepwise/step-11-project-inventory-build-notes.md`, `stepwise/step-11-decision-tree-v2.html`.

**Carried out by:** OpenCode.

**What it does:** asks whether the application is new or existing, and its slug, then checks the ledger is reachable. For a new application it asks for the GitHub code repository (Anvil creates it; the agent never does), copies the project template to `C:\dev\dev-{slug}\`, links the code repository, creates the documentation repository on GitHub with the developer's permission, and asks the developer to supply the three pre-project files. For an existing application it asks for both GitHub repositories and both local paths, creates only missing folders, and checks the GitHub and GBrain links, correcting them only with permission; the developer then confirms the data is sound. Both routes then set up `AGENTS.md`, the system files and the Matt Pocock skills configuration, register both repositories in GBrain, check that `project-library-global` is registered, insert the application's row in the ledger, and audit everything, correcting nothing without permission.

**Produces:** the two repositories on disk, linked to GitHub; their GBrain sources; the `projects` ledger row; the pre-project files in `dev-{slug}\{slug}-project-library\pre-project\` (new applications); the Step Receipt at `dev-{slug}\{slug}-project-library\pdlf\step-11-receipt.md`.

**BFT level:** Full.

**Decided while building:** one procedure for both entry routes, which differ only in how the repositories are obtained; the old existing-project audit (Steps 2 and 3, SKIP / RE-RUN / RUN-AS-NEW) is retired, because an existing application is redeveloped around its concept, not audited; global reference files are never copied into a project; no git operation ever runs without permission; folders created for an existing application get no `Instructions.md`.

#### Step 12: Office hours

**Status:** Built. Last changed 2026-08-25.

**Files:** `stepwise/step-12-office-hours.md` (the step), `stepwise/step-12-build-notes.md`, `stepwise/step-12-decision-tree.html`.

**Carried out by:** OpenCode, with GStack `/office-hours` if the developer chooses.

**What it does:** searches GBrain, then gathers the concept. For a new application it reads the three pre-project files and questions the developer until the scope is clear. For an existing application it reads the whole existing documentation through GBrain, separates the durable concept from what followed from it, shows any document that already claims to state the concept, and proposes the split for the developer to confirm or correct. It then always writes a design doc (problem, demand, status quo, target user, constraints, approaches, recommendation, open questions, success criteria) and asks whether to run `/office-hours`. If yes, the draft is pasted into `/office-hours` in full, which skips its interview but still challenges the premise and the alternatives; its result becomes the working design doc.

**Produces:** `docs-local\design-doc-first-concept.md` (written once and never changed, kept to check later for concept drift), `docs-local\design-doc.md` (the working copy), the `/office-hours` file at its own GStack location if it ran, and the Step Receipt. The ledger records whether the design doc was synthesized (`/office-hours` declined), which puts an input notice on later steps.

**BFT level:** Full.

**Decided while building:** the draft must be pasted into `/office-hours` itself, because the skill does not read the project's folders; the first-concept file is a fourth item handed to Step 14.

#### Step 13: Not used

**Status:** Not used.

#### Step 14: CEO review

**Status:** Built. Last changed 2026-08-25.

**Files:** `stepwise/step-14-plan-ceo-review.md` (the step), `stepwise/step-14-build-notes.md`, `stepwise/step-14-decision-tree.html`.

**Carried out by:** GStack `/plan-ceo-review`.

**What it does:** searches GBrain, checks whether Step 12's design doc was synthesized, and pastes Step 12's four handed-over items into the skill in full, stating that a design doc already exists, so that the skill does not offer to rerun `/office-hours`. Before invoking it, OpenCode compares the project's material with `project-library-global`: the global standard wins unless the developer approves a deviation. The skill then challenges the premise, the developer chooses one of four scope modes (expansion, selective expansion, hold scope, reduction), and the skill works through an 11-section review, putting each finding to the developer one at a time.

**Produces:** the CEO plan, written by the skill to its own GStack location only in the two expansion modes; in the other two modes OpenCode saves the review itself. A stable copy is kept in the project, plus the Step Receipt.

**BFT level:** Full.

**Decided while building:** no branch on how Step 12 produced its design doc; the skill's own design-doc search and save path were read from its source, not assumed; the comparison with `project-library-global` is OpenCode's, because the skill knows nothing of it.

#### Step 15: Engineering review

**Status:** Built. Last changed 2026-08-25.

**Files:** `stepwise/step-15-plan-eng-review.md` (the step), `stepwise/step-15-build-notes.md`, `stepwise/step-15-decision-tree.html`.

**Carried out by:** GStack `/plan-eng-review`.

**What it does:** searches GBrain, finds Step 14's plan according to the scope mode used, and pastes it with the design docs into the skill, stating that a design doc already exists. OpenCode makes the same comparison with `project-library-global` as at Step 14. The skill runs its scope challenge, which stops for the developer if the plan touches 8 or more files or 2 or more new services, then four reviews (architecture, code quality, tests and performance), each finding put to the developer one at a time. It writes a test plan, adds its required outputs (what is out of scope, what already exists, diagrams, failure modes) to the plan, gets a second opinion from another AI, and ends with its review report.

**Produces:** the reviewed plan and the test plan (used later by Steps 35 and 38), with stable copies in the project, plus the Step Receipt.

**BFT level:** Full.

**Decided while building:** the skill produces one separate file, the test plan, not the five architecture documents earlier drafts assumed; whether the skill finds "the active plan file" inside OpenCode is to be watched on the first live run, and does not block the step, because OpenCode captures the findings itself.

#### Step 16: Domain modeling

**Status:** Built. Last changed 2026-08-27.

**Files:** `stepwise/step-16-domain-modeling.md` (the step), `stepwise/step-16-build-notes.md`, `stepwise/step-16-decision-tree.html`.

**Carried out by:** Matt Pocock `/grill-with-docs`, which runs a `/grilling` interview using `/domain-modeling`.

**What it does:** searches GBrain and pastes Step 15's plan and test plan into the skill, with the existing `CONTEXT.md`, decision records and code for an existing application. The interview walks the plan one decision at a time, gives a recommended answer, and waits for the developer. As each term is settled it is written to `CONTEXT.md` at once; a decision record is offered only for a decision that is hard to reverse, surprising without context and the result of a real trade-off. The security review `mb-sentinel-review` then checks whether any sensitive data or security-relevant entities were created; a finding stops the step and goes to the developer before the gate. The step checks that the files exist and that the security review left its record in the ledger, then runs the gate.

**Produces:** `CONTEXT.md` (the glossary) and any decision records in `adr-local\`, in the documentation repository, plus the Step Receipt.

**Gate:** `domain-locked`, with full BFT; nothing further happens until the developer approves.

**Decided while building:** `/domain-modeling` cannot run on its own, so the step invokes `/grill-with-docs`; the skill's default file locations are overridden to the project's own; no separate reconciliation mode is needed for an existing application, because the skill checks the code whenever code exists; the security review was added before the gate, and its run is proven by its ledger record, not assumed.

### Phase B — Design and Plan

#### Step 17: Create Anvil data tables

**File:** `stepwise/step-17-create-anvil-data-tables.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 18: Pull to local

**File:** `stepwise/step-18-pull-to-local.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 19: To tickets

**File:** `stepwise/step-19-to-tickets.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 20: Design consultation

**File:** `stepwise/step-20-design-consultation.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 21: Concept sanity audit

**File:** `stepwise/step-21-concept-sanity-audit.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 22: Wireframes, phase 1

**File:** `stepwise/step-22-wireframe-phase-1.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 23: Plan design review

**File:** `stepwise/step-23-plan-design-review.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 24: Plan developer-experience review

**File:** `stepwise/step-24-plan-devex-review.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 25: Not used

**Status:** Not used.

#### Step 26: Wireframes, phase 2

**File:** `stepwise/step-26-wireframe-phase-2.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 27: Screen production

**File:** `stepwise/step-27-screen-production.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 28: Screen to PNG

**File:** `stepwise/step-28-screen-to-png.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

### Phase C — Scaffold and Assemble

#### Step 29: Build UI forms

**File:** `stepwise/step-29-build-ui-forms.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 30: Pull to local

**File:** `stepwise/step-30-pull-to-local.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 31: Scaffold planning

**File:** `stepwise/step-31-scaffold-planning.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 32: Physical scaffold build

**File:** `stepwise/step-32-physical-scaffold-build.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 33: Pull to local

**File:** `stepwise/step-33-pull-to-local.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 34: Architectural sanity audit

**File:** `stepwise/step-34-architectural-sanity-audit.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

### Phase D — Build and Verify

#### Step 35: Build

**File:** `stepwise/step-35-build-loop.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 35A: Testing

**File:** `stepwise/step-35A-testing.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 36: Design review

**File:** `stepwise/step-36-design-review.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 37: Code review

**File:** `stepwise/step-37-review.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 38: Quality testing

**File:** `stepwise/step-38-qa.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 38A: Dependency check

**File:** `stepwise/step-38A-dependency-scan-confirm.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 39: Triage

**File:** `stepwise/step-39-triage.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 40: Architecture scan

**File:** `stepwise/step-40-improve-codebase-architecture.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 40B: Approved fixes

**File:** `stepwise/step-40B-remediation.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

### Phase E — Ship and Monitor

#### Step 41: Ship

**File:** `stepwise/step-41-ship.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 42: Publish to staging

**File:** `stepwise/step-42-publish-to-staging.md`

**Status:** Old draft. Still describes staging, which PDLF does not have; to be rebuilt.

#### Step 42A: Staging integration tests

**File:** `stepwise/step-42A-staging-integration-e2e.md`

**Status:** Old draft. Still describes staging, which PDLF does not have; to be rebuilt.

#### Step 43: Staging smoke test

**File:** `stepwise/step-43-staging-smoke-test.md`

**Status:** Old draft. Still describes staging, which PDLF does not have; to be rebuilt.

#### Step 44: Release

**File:** `stepwise/step-44-promote-to-production.md`

**Status:** Old draft. Still describes staging, which PDLF does not have; to be rebuilt.

#### Step 45: Production check

**File:** `stepwise/step-45-canary-production.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 46: Learning

**File:** `stepwise/step-46-LEARN-junction.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

### After Step 46: the remaining apps

**File:** none.

**Status:** Not yet designed.
