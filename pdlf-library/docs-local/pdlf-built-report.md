---
title: "pdlf-built-report"
doc-id: "mb-36208a1a"
updated: "2026-10-24"
---
# PDLF Built Report

## Preamble

This document records what has been built of PDLF so far, step by step. For each step it states the step's status and its files, and links the step's explainer and configuration, which say what the step does and what it produces. What each step must achieve is in its own build plan; this report never repeats it.

The steps are listed in the same order and under the same phases as the build plan, so the two can be read side by side. Every step has an entry, whether or not any work has been done on it yet, so that each piece of work is recorded in its place as it happens.

Each entry is updated whenever its step is built, corrected or packaged. A step has one of four statuses: **not yet built**; **built** (Pass 1: its build plan is closed and its test specification, configuration, reference, explainer and decision tree are written); **proven** (Pass 2: `mb-3-cs` has run through it); **finished** (Pass 3: its module is written).

This report is a working tool for building PDLF. It is deleted when PDLF is finished.

## The Built Report

### Phase A — Init

#### Step 1: Orchestrator

**File:** `app-factory/phase-a-init/01-orchestrator.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet designed.

#### Steps 2 to 10: Entry points

**Files:** `app-factory/phase-a-init/04-undefined.md` to `10-undefined.md` (placeholders; 2 and 3 have no file).

**Status:** Not yet designed.

### Phase B — Discover and Define

#### Step 11: Init

**Status:** Built.

**Files:** in `app-factory/phase-b-discover-and-define/`: `b11-build-plan.md`, `b11-test-spec.md`, `b11-config.md`, `b11-reference.md`, `b11-explainer.md`, `b11-decision-tree.html`, `b11-module.md` (empty until Pass 3).

**What it does and produces:** [[[pdlf:app-factory/phase-b-discover-and-define/b11-explainer|Step 11 Explainer]]](C:/pdlf/app-factory/phase-b-discover-and-define/b11-explainer.md); [[[pdlf:app-factory/phase-b-discover-and-define/b11-config|Step 11 Configuration]]](C:/pdlf/app-factory/phase-b-discover-and-define/b11-config.md).

#### Step 12: Office hours

**Status:** Built.

**Files:** in `app-factory/phase-b-discover-and-define/`: `b12-build-plan.md`, `b12-test-spec.md`, `b12-config.md`, `b12-reference.md`, `b12-explainer.md`, `b12-decision-tree.html`, `b12-module.md` (empty until Pass 3).

**What it does and produces:** [[[pdlf:app-factory/phase-b-discover-and-define/b12-explainer|Step 12 Explainer]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-explainer.md); [[[pdlf:app-factory/phase-b-discover-and-define/b12-config|Step 12 Configuration]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-config.md).

#### Step 13: Not used

**Status:** Not used.

#### Step 14: CEO review

**Status:** Built.

**Files:** in `app-factory/phase-b-discover-and-define/`: `b14-build-plan.md`, `b14-test-spec.md`, `b14-config.md`, `b14-reference.md`, `b14-explainer.md`, `b14-decision-tree.html`, `b14-module.md` (empty until Pass 3).

**What it does and produces:** [[[pdlf:app-factory/phase-b-discover-and-define/b14-explainer|Step 14 Explainer]]](C:/pdlf/app-factory/phase-b-discover-and-define/b14-explainer.md); [[[pdlf:app-factory/phase-b-discover-and-define/b14-config|Step 14 Configuration]]](C:/pdlf/app-factory/phase-b-discover-and-define/b14-config.md).

#### Step 15: Engineering review

**Status:** Built. Last changed 2026-08-25.

**Files:** `app-factory/phase-b-discover-and-define/15-plan-eng-review.md` (the step), `app-factory/phase-b-discover-and-define/15-build-notes.md`, `app-factory/phase-b-discover-and-define/15-decision-tree.html`.

**Carried out by:** GStack `/plan-eng-review`.

**What it does:** searches GBrain, finds Step 14's plan according to the scope mode used, and pastes it with the design docs into the skill, stating that a design doc already exists. OpenCode makes the same comparison with `project-library-global` as at Step 14. The skill runs its scope challenge, which stops for the developer if the plan touches 8 or more files or 2 or more new services, then four reviews (architecture, code quality, tests and performance), each finding put to the developer one at a time. It writes a test plan, adds its required outputs (what is out of scope, what already exists, diagrams, failure modes) to the plan, gets a second opinion from another AI, and ends with its review report.

**Produces:** the reviewed plan and the test plan (used later by Steps 35 and 38), with stable copies in the project, plus the Step Receipt.

**BFT level:** Full.

**Decided while building:** the skill produces one separate file, the test plan, not the five architecture documents earlier drafts assumed; whether the skill finds "the active plan file" inside OpenCode is to be watched on the first live run, and does not block the step, because OpenCode captures the findings itself.

#### Step 16: Domain modeling

**Status:** Built. Last changed 2026-08-27.

**Files:** `app-factory/phase-b-discover-and-define/16-domain-modeling.md` (the step), `app-factory/phase-b-discover-and-define/16-build-notes.md`, `app-factory/phase-b-discover-and-define/16-decision-tree.html`.

**Carried out by:** Matt Pocock `/grill-with-docs`, which runs a `/grilling` interview using `/domain-modeling`.

**What it does:** searches GBrain and pastes Step 15's plan and test plan into the skill, with the existing `CONTEXT.md`, decision records and code for an existing application. The interview walks the plan one decision at a time, gives a recommended answer, and waits for the developer. As each term is settled it is written to `CONTEXT.md` at once; a decision record is offered only for a decision that is hard to reverse, surprising without context and the result of a real trade-off. The security review `mb-sentinel-review` then checks whether any sensitive data or security-relevant entities were created; a finding stops the step and goes to the developer before the gate. The step checks that the files exist and that the security review left its record in the ledger, then runs the gate.

**Produces:** `CONTEXT.md` (the glossary) and any decision records in `adr-local\`, in the documentation repository, plus the Step Receipt.

**Gate:** `domain-locked`, with full BFT; nothing further happens until the developer approves.

**Decided while building:** `/domain-modeling` cannot run on its own, so the step invokes `/grill-with-docs`; the skill's default file locations are overridden to the project's own; no separate reconciliation mode is needed for an existing application, because the skill checks the code whenever code exists; the security review was added before the gate, and its run is proven by its ledger record, not assumed.

### Phase C — Design and Plan

#### Step 17: Create Anvil data tables

**File:** `app-factory/phase-c-design-and-plan/17-create-anvil-data-tables.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 18: Pull to local

**File:** `app-factory/phase-c-design-and-plan/18-pull-to-local.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 19: To tickets

**File:** `app-factory/phase-c-design-and-plan/19-to-tickets.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 20: Design consultation

**File:** `app-factory/phase-c-design-and-plan/20-design-consultation.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 21: Concept sanity audit

**File:** `app-factory/phase-c-design-and-plan/21-concept-sanity-audit.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 22: Wireframes, phase 1

**File:** `app-factory/phase-c-design-and-plan/22-wireframe-phase-1.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 23: Plan design review

**File:** `app-factory/phase-c-design-and-plan/23-plan-design-review.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 24: Plan developer-experience review

**File:** `app-factory/phase-c-design-and-plan/24-plan-devex-review.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 25: Not used

**Status:** Not used.

#### Step 26: Wireframes, phase 2

**File:** `app-factory/phase-c-design-and-plan/26-wireframe-phase-2.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 27: Screen production

**File:** `app-factory/phase-c-design-and-plan/27-screen-production.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 28: Screen to PNG

**File:** `app-factory/phase-c-design-and-plan/28-screen-to-png.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

### Phase D — Scaffold and Assemble

#### Step 29: Build UI forms

**File:** `app-factory/phase-d-scaffold-and-assemble/29-build-ui-forms.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 30: Pull to local

**File:** `app-factory/phase-d-scaffold-and-assemble/30-pull-to-local.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 31: Scaffold planning

**File:** `app-factory/phase-d-scaffold-and-assemble/31-scaffold-planning.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 32: Physical scaffold build

**File:** `app-factory/phase-d-scaffold-and-assemble/32-physical-scaffold-build.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 33: Pull to local

**File:** `app-factory/phase-d-scaffold-and-assemble/33-pull-to-local.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 34: Architectural sanity audit

**File:** `app-factory/phase-d-scaffold-and-assemble/34-architectural-sanity-audit.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

### Phase E — Build and Verify

#### Step 35: Build

**File:** `app-factory/phase-e-build-and-verify/35-build-loop.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 35A: Testing

**File:** `app-factory/phase-e-build-and-verify/35a-testing.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 36: Design review

**File:** `app-factory/phase-e-build-and-verify/36-design-review.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 37: Code review

**File:** `app-factory/phase-e-build-and-verify/37-review.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 38: Quality testing

**File:** `app-factory/phase-e-build-and-verify/38-qa.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 38A: Dependency check

**File:** `app-factory/phase-e-build-and-verify/38a-dependency-scan-confirm.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 39: Triage

**File:** `app-factory/phase-e-build-and-verify/39-triage.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 40: Architecture scan

**File:** `app-factory/phase-e-build-and-verify/40-improve-codebase-architecture.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 40B: Approved fixes

**File:** `app-factory/phase-e-build-and-verify/40b-remediation.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

### Phase F — Ship and Monitor

#### Step 41: Ship

**File:** `app-factory/phase-f-ship-and-monitor/41-ship.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 42: Publish to staging

**File:** `app-factory/phase-f-ship-and-monitor/42-publish-to-staging.md`

**Status:** Old draft. Still describes staging, which PDLF does not have; to be rebuilt.

#### Step 42A: Staging integration tests

**File:** `app-factory/phase-f-ship-and-monitor/42a-staging-integration-e2e.md`

**Status:** Old draft. Still describes staging, which PDLF does not have; to be rebuilt.

#### Step 43: Staging smoke test

**File:** `app-factory/phase-f-ship-and-monitor/43-staging-smoke-test.md`

**Status:** Old draft. Still describes staging, which PDLF does not have; to be rebuilt.

#### Step 44: Release

**File:** `app-factory/phase-f-ship-and-monitor/44-promote-to-production.md`

**Status:** Old draft. Still describes staging, which PDLF does not have; to be rebuilt.

#### Step 45: Production check

**File:** `app-factory/phase-f-ship-and-monitor/45-canary-production.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

#### Step 46: Learning

**File:** `app-factory/phase-f-ship-and-monitor/46-learn-junction.md`

**Status:** Old draft, written before `pdlf-intent.md`. Not yet rebuilt.

### Phase G — Remaining apps

**File:** none.

**Status:** Not yet designed.
