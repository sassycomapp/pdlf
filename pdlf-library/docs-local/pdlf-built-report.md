---
title: "pdlf-built-report"
doc-id: "mb-36208a1a"
updated: "2026-11-13"
---
# PDLF Built Report

## Preamble

This document records what has been built of PDLF so far, step by step. For each step it states the step's status and its files, and links the step's explainer and configuration, which say what the step does and what it produces. What each step must achieve is in its own build plan; this report never repeats it.

The steps are listed in the same order and under the same phases as the build plan, so the two can be read side by side. Every step has an entry, whether or not any work has been done on it yet, so that each piece of work is recorded in its place as it happens.

Each entry is updated whenever its step is built, corrected or packaged. A step has one of four statuses: **not yet built**; **built** (its build plan is closed and its test specification, configuration, reference, explainer and decision tree are written); **proven** (`mb-3-cs` has run through it); **finished** (its module is written). The order in which the phases reach each status is set out in the [[[pdlf:pdlf-library/docs-local/app-factory-docs-update-method|App Factory Docs Update Method]]](C:/pdlf/pdlf-library/docs-local/app-factory-docs-update-method.md).

This report is a working tool for building PDLF. It is deleted when PDLF is finished.

## The Built Report

### Phase A — Init

**Phase status:** Built, for Phases A and B: every entry point and the orchestrator as far as it runs Phases A and B. Phase A has no gate.

#### Step 1: Orchestrator

**Files:** in `app-factory/phase-a-init/`: `a01-build-plan.md`, `a01-test-spec.md`, `a01-config.md`, `a01-reference.md`, `a01-explainer.md`, `a01-decision-tree.html`, `a01-module.md`.

**Status:** Built, as far as it runs Phases A and B, with the resume check. It is extended with each later phase.

**What it does and produces:** [[[pdlf:app-factory/phase-a-init/a01-explainer|Step 1 Explainer]]](C:/pdlf/app-factory/phase-a-init/a01-explainer.md); [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md). Its launcher skill is `pdlf-library/skills-local/pdlf-init/SKILL.md`.

#### Steps 2 to 10: Entry points

**Files:** in `app-factory/phase-a-init/`: the suites `a02` to `a10`, seven files each.

**Status:** Built. Each is proven the first time a run takes it.

**What they do and produce:** each entry point's explainer and configuration, `a02-explainer.md` to `a10-explainer.md` and `a02-config.md` to `a10-config.md`; the values they share are in [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md).

### Phase B — Discover and Define

**Phase status:** Proven: every step of the phase has run on `mb-3-cs`, and the run passed the gate `domain-locked` (Step 16).

#### Step 11: Init

**Status:** Proven on `mb-3-cs` (route B), with the faults found corrected in its documents, the test tools and Cupcake.

**Files:** in `app-factory/phase-b-discover-and-define/`: `b11-build-plan.md`, `b11-test-spec.md`, `b11-config.md`, `b11-reference.md`, `b11-explainer.md`, `b11-decision-tree.html`, `b11-module.md` (empty until the step is proven).

**What it does and produces:** [[[pdlf:app-factory/phase-b-discover-and-define/b11-explainer|Step 11 Explainer]]](C:/pdlf/app-factory/phase-b-discover-and-define/b11-explainer.md); [[[pdlf:app-factory/phase-b-discover-and-define/b11-config|Step 11 Configuration]]](C:/pdlf/app-factory/phase-b-discover-and-define/b11-config.md).

#### Step 12: Office hours

**Status:** Proven on `mb-3-cs`.

**Files:** in `app-factory/phase-b-discover-and-define/`: `b12-build-plan.md`, `b12-test-spec.md`, `b12-config.md`, `b12-reference.md`, `b12-explainer.md`, `b12-decision-tree.html`, `b12-module.md` (empty until the step is proven).

**What it does and produces:** [[[pdlf:app-factory/phase-b-discover-and-define/b12-explainer|Step 12 Explainer]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-explainer.md); [[[pdlf:app-factory/phase-b-discover-and-define/b12-config|Step 12 Configuration]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-config.md).

#### Step 13: Not used

**Status:** Not used.

#### Step 14: CEO review

**Status:** Proven on `mb-3-cs`.

**Files:** in `app-factory/phase-b-discover-and-define/`: `b14-build-plan.md`, `b14-test-spec.md`, `b14-config.md`, `b14-reference.md`, `b14-explainer.md`, `b14-decision-tree.html`, `b14-module.md` (empty until the step is proven).

**What it does and produces:** [[[pdlf:app-factory/phase-b-discover-and-define/b14-explainer|Step 14 Explainer]]](C:/pdlf/app-factory/phase-b-discover-and-define/b14-explainer.md); [[[pdlf:app-factory/phase-b-discover-and-define/b14-config|Step 14 Configuration]]](C:/pdlf/app-factory/phase-b-discover-and-define/b14-config.md).

#### Step 15: Engineering review

**Status:** Proven on `mb-3-cs`.

**Files:** in `app-factory/phase-b-discover-and-define/`: `b15-build-plan.md`, `b15-test-spec.md`, `b15-config.md`, `b15-reference.md`, `b15-explainer.md`, `b15-decision-tree.html`, `b15-module.md` (empty until the step is proven).

**What it does and produces:** [[[pdlf:app-factory/phase-b-discover-and-define/b15-explainer|Step 15 Explainer]]](C:/pdlf/app-factory/phase-b-discover-and-define/b15-explainer.md); [[[pdlf:app-factory/phase-b-discover-and-define/b15-config|Step 15 Configuration]]](C:/pdlf/app-factory/phase-b-discover-and-define/b15-config.md).

#### Step 16: Domain modeling

**Status:** Proven on `mb-3-cs`.

**Files:** in `app-factory/phase-b-discover-and-define/`: `b16-build-plan.md`, `b16-test-spec.md`, `b16-config.md`, `b16-reference.md`, `b16-explainer.md`, `b16-decision-tree.html`, `b16-module.md` (empty until the step is proven).

**What it does and produces:** [[[pdlf:app-factory/phase-b-discover-and-define/b16-explainer|Step 16 Explainer]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-explainer.md); [[[pdlf:app-factory/phase-b-discover-and-define/b16-config|Step 16 Configuration]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-config.md).

### Phase C — Design and Plan

**Phase status:** Built: every step of the phase is written to `mo-ui-production`, and the orchestrator runs it. Not yet proven: `mb-3-cs` has not yet run through it.

#### Step 17: Create Anvil data tables

**Status:** Built.

**Files:** in `app-factory/phase-c-design-and-plan/`: `c17-build-plan.md`, `c17-test-spec.md`, `c17-config.md`, `c17-reference.md`, `c17-explainer.md`, `c17-decision-tree.html`, `c17-module.md` (empty until the step is packaged).

**What it does and produces:** [[[pdlf:app-factory/phase-c-design-and-plan/c17-explainer|Step 17 Explainer]]](C:/pdlf/app-factory/phase-c-design-and-plan/c17-explainer.md); [[[pdlf:app-factory/phase-c-design-and-plan/c17-config|Step 17 Configuration]]](C:/pdlf/app-factory/phase-c-design-and-plan/c17-config.md).

#### Step 18: Pull to local

**Status:** Built.

**Files:** in `app-factory/phase-c-design-and-plan/`: `c18-build-plan.md`, `c18-test-spec.md`, `c18-config.md`, `c18-reference.md`, `c18-explainer.md`, `c18-decision-tree.html`, `c18-module.md` (empty until the step is packaged).

**What it does and produces:** [[[pdlf:app-factory/phase-c-design-and-plan/c18-explainer|Step 18 Explainer]]](C:/pdlf/app-factory/phase-c-design-and-plan/c18-explainer.md); [[[pdlf:app-factory/phase-c-design-and-plan/c18-config|Step 18 Configuration]]](C:/pdlf/app-factory/phase-c-design-and-plan/c18-config.md).

#### Step 19: Tickets

**Status:** Built.

**Files:** in `app-factory/phase-c-design-and-plan/`: `c19-build-plan.md`, `c19-test-spec.md`, `c19-config.md`, `c19-reference.md`, `c19-explainer.md`, `c19-decision-tree.html`, `c19-module.md` (empty until the step is packaged).

**What it does and produces:** [[[pdlf:app-factory/phase-c-design-and-plan/c19-explainer|Step 19 Explainer]]](C:/pdlf/app-factory/phase-c-design-and-plan/c19-explainer.md); [[[pdlf:app-factory/phase-c-design-and-plan/c19-config|Step 19 Configuration]]](C:/pdlf/app-factory/phase-c-design-and-plan/c19-config.md).

#### Step 20: Design system

**Status:** Built.

**Files:** in `app-factory/phase-c-design-and-plan/`: `c20-build-plan.md`, `c20-test-spec.md`, `c20-config.md`, `c20-reference.md`, `c20-explainer.md`, `c20-decision-tree.html`, `c20-module.md` (empty until the step is packaged).

**What it does and produces:** [[[pdlf:app-factory/phase-c-design-and-plan/c20-explainer|Step 20 Explainer]]](C:/pdlf/app-factory/phase-c-design-and-plan/c20-explainer.md); [[[pdlf:app-factory/phase-c-design-and-plan/c20-config|Step 20 Configuration]]](C:/pdlf/app-factory/phase-c-design-and-plan/c20-config.md).

#### Step 21: Concept check

**Status:** Built.

**Files:** in `app-factory/phase-c-design-and-plan/`: `c21-build-plan.md`, `c21-test-spec.md`, `c21-config.md`, `c21-reference.md`, `c21-explainer.md`, `c21-decision-tree.html`, `c21-module.md` (empty until the step is packaged).

**What it does and produces:** [[[pdlf:app-factory/phase-c-design-and-plan/c21-explainer|Step 21 Explainer]]](C:/pdlf/app-factory/phase-c-design-and-plan/c21-explainer.md); [[[pdlf:app-factory/phase-c-design-and-plan/c21-config|Step 21 Configuration]]](C:/pdlf/app-factory/phase-c-design-and-plan/c21-config.md).

#### Step 22: Screen requirements

**Status:** Built.

**Files:** in `app-factory/phase-c-design-and-plan/`: `c22-build-plan.md`, `c22-test-spec.md`, `c22-config.md`, `c22-reference.md`, `c22-explainer.md`, `c22-decision-tree.html`, `c22-module.md` (empty until the step is packaged).

**What it does and produces:** [[[pdlf:app-factory/phase-c-design-and-plan/c22-explainer|Step 22 Explainer]]](C:/pdlf/app-factory/phase-c-design-and-plan/c22-explainer.md); [[[pdlf:app-factory/phase-c-design-and-plan/c22-config|Step 22 Configuration]]](C:/pdlf/app-factory/phase-c-design-and-plan/c22-config.md).

#### Step 23: Design review

**Status:** Built.

**Files:** in `app-factory/phase-c-design-and-plan/`: `c23-build-plan.md`, `c23-test-spec.md`, `c23-config.md`, `c23-reference.md`, `c23-explainer.md`, `c23-decision-tree.html`, `c23-module.md` (empty until the step is packaged).

**What it does and produces:** [[[pdlf:app-factory/phase-c-design-and-plan/c23-explainer|Step 23 Explainer]]](C:/pdlf/app-factory/phase-c-design-and-plan/c23-explainer.md); [[[pdlf:app-factory/phase-c-design-and-plan/c23-config|Step 23 Configuration]]](C:/pdlf/app-factory/phase-c-design-and-plan/c23-config.md).

#### Step 24: Not used

**Status:** Not used.

#### Step 25: Not used

**Status:** Not used.

#### Step 26: Screens approved

**Status:** Built.

**Files:** in `app-factory/phase-c-design-and-plan/`: `c26-build-plan.md`, `c26-test-spec.md`, `c26-config.md`, `c26-reference.md`, `c26-explainer.md`, `c26-decision-tree.html`, `c26-module.md` (empty until the step is packaged).

**What it does and produces:** [[[pdlf:app-factory/phase-c-design-and-plan/c26-explainer|Step 26 Explainer]]](C:/pdlf/app-factory/phase-c-design-and-plan/c26-explainer.md); [[[pdlf:app-factory/phase-c-design-and-plan/c26-config|Step 26 Configuration]]](C:/pdlf/app-factory/phase-c-design-and-plan/c26-config.md).

#### Step 27: Not used

**Status:** Not used.

#### Step 28: Not used

**Status:** Not used.

### Phase D — Scaffold and Assemble

**Phase status:** Built: every step of the phase is written to the current intent, and the orchestrator runs it. Not yet proven.

#### Step 29: Not used

**Status:** Not used.

#### Step 30: Not used

**Status:** Not used.

#### Step 31: Scaffold plan

**Status:** Built.

**Files:** in `app-factory/phase-d-scaffold-and-assemble/`: `d31-build-plan.md`, `d31-test-spec.md`, `d31-config.md`, `d31-reference.md`, `d31-explainer.md`, `d31-decision-tree.html`, `d31-module.md` (empty until the step is packaged).

**What it does and produces:** [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d31-explainer|Step 31 Explainer]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d31-explainer.md); [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d31-config|Step 31 Configuration]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d31-config.md).

#### Step 32: Create the scaffold

**Status:** Built.

**Files:** in `app-factory/phase-d-scaffold-and-assemble/`: `d32-build-plan.md`, `d32-test-spec.md`, `d32-config.md`, `d32-reference.md`, `d32-explainer.md`, `d32-decision-tree.html`, `d32-module.md` (empty until the step is packaged).

**What it does and produces:** [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d32-explainer|Step 32 Explainer]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d32-explainer.md); [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d32-config|Step 32 Configuration]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d32-config.md).

#### Step 33: Pull to local

**Status:** Built.

**Files:** in `app-factory/phase-d-scaffold-and-assemble/`: `d33-build-plan.md`, `d33-test-spec.md`, `d33-config.md`, `d33-reference.md`, `d33-explainer.md`, `d33-decision-tree.html`, `d33-module.md` (empty until the step is packaged).

**What it does and produces:** [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d33-explainer|Step 33 Explainer]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d33-explainer.md); [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d33-config|Step 33 Configuration]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d33-config.md).

#### Step 34: Architecture audit

**Status:** Built.

**Files:** in `app-factory/phase-d-scaffold-and-assemble/`: `d34-build-plan.md`, `d34-test-spec.md`, `d34-config.md`, `d34-reference.md`, `d34-explainer.md`, `d34-decision-tree.html`, `d34-module.md` (empty until the step is packaged).

**What it does and produces:** [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d34-explainer|Step 34 Explainer]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d34-explainer.md); [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d34-config|Step 34 Configuration]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d34-config.md).

### Phase E — Build and Verify

**Phase status:** Built: every step of the phase is written to the current intent, runs once per ticket, and the orchestrator runs it. Not yet proven.

#### Step 35: Build

**Status:** Built.

**Files:** in `app-factory/phase-e-build-and-verify/`: `e35-build-plan.md`, `e35-test-spec.md`, `e35-config.md`, `e35-reference.md`, `e35-explainer.md`, `e35-decision-tree.html`, `e35-module.md` (empty until the step is packaged).

**What it does and produces:** [[[pdlf:app-factory/phase-e-build-and-verify/e35-explainer|Step 35 Explainer]]](C:/pdlf/app-factory/phase-e-build-and-verify/e35-explainer.md); [[[pdlf:app-factory/phase-e-build-and-verify/e35-config|Step 35 Configuration]]](C:/pdlf/app-factory/phase-e-build-and-verify/e35-config.md).

#### Step 35A: Testing

**Status:** Built.

**Files:** in `app-factory/phase-e-build-and-verify/`: `e35a-build-plan.md`, `e35a-test-spec.md`, `e35a-config.md`, `e35a-reference.md`, `e35a-explainer.md`, `e35a-decision-tree.html`, `e35a-module.md` (empty until the step is packaged).

**What it does and produces:** [[[pdlf:app-factory/phase-e-build-and-verify/e35a-explainer|Step 35A Explainer]]](C:/pdlf/app-factory/phase-e-build-and-verify/e35a-explainer.md); [[[pdlf:app-factory/phase-e-build-and-verify/e35a-config|Step 35A Configuration]]](C:/pdlf/app-factory/phase-e-build-and-verify/e35a-config.md).

#### Step 40: Architecture scan

**Status:** Built.

**Files:** in `app-factory/phase-e-build-and-verify/`: `e40-build-plan.md`, `e40-test-spec.md`, `e40-config.md`, `e40-reference.md`, `e40-explainer.md`, `e40-decision-tree.html`, `e40-module.md` (empty until the step is packaged).

**What it does and produces:** [[[pdlf:app-factory/phase-e-build-and-verify/e40-explainer|Step 40 Explainer]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40-explainer.md); [[[pdlf:app-factory/phase-e-build-and-verify/e40-config|Step 40 Configuration]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40-config.md).

#### Step 40B: Approved fixes

**Status:** Built.

**Files:** in `app-factory/phase-e-build-and-verify/`: `e40b-build-plan.md`, `e40b-test-spec.md`, `e40b-config.md`, `e40b-reference.md`, `e40b-explainer.md`, `e40b-decision-tree.html`, `e40b-module.md` (empty until the step is packaged).

**What it does and produces:** [[[pdlf:app-factory/phase-e-build-and-verify/e40b-explainer|Step 40B Explainer]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40b-explainer.md); [[[pdlf:app-factory/phase-e-build-and-verify/e40b-config|Step 40B Configuration]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40b-config.md).

#### Step 36: Design review

**Status:** Built.

**Files:** in `app-factory/phase-e-build-and-verify/`: `e36-build-plan.md`, `e36-test-spec.md`, `e36-config.md`, `e36-reference.md`, `e36-explainer.md`, `e36-decision-tree.html`, `e36-module.md` (empty until the step is packaged).

**What it does and produces:** [[[pdlf:app-factory/phase-e-build-and-verify/e36-explainer|Step 36 Explainer]]](C:/pdlf/app-factory/phase-e-build-and-verify/e36-explainer.md); [[[pdlf:app-factory/phase-e-build-and-verify/e36-config|Step 36 Configuration]]](C:/pdlf/app-factory/phase-e-build-and-verify/e36-config.md).

#### Step 37: Code review

**Status:** Built.

**Files:** in `app-factory/phase-e-build-and-verify/`: `e37-build-plan.md`, `e37-test-spec.md`, `e37-config.md`, `e37-reference.md`, `e37-explainer.md`, `e37-decision-tree.html`, `e37-module.md` (empty until the step is packaged).

**What it does and produces:** [[[pdlf:app-factory/phase-e-build-and-verify/e37-explainer|Step 37 Explainer]]](C:/pdlf/app-factory/phase-e-build-and-verify/e37-explainer.md); [[[pdlf:app-factory/phase-e-build-and-verify/e37-config|Step 37 Configuration]]](C:/pdlf/app-factory/phase-e-build-and-verify/e37-config.md).

#### Step 38: Quality testing

**Status:** Built.

**Files:** in `app-factory/phase-e-build-and-verify/`: `e38-build-plan.md`, `e38-test-spec.md`, `e38-config.md`, `e38-reference.md`, `e38-explainer.md`, `e38-decision-tree.html`, `e38-module.md` (empty until the step is packaged).

**What it does and produces:** [[[pdlf:app-factory/phase-e-build-and-verify/e38-explainer|Step 38 Explainer]]](C:/pdlf/app-factory/phase-e-build-and-verify/e38-explainer.md); [[[pdlf:app-factory/phase-e-build-and-verify/e38-config|Step 38 Configuration]]](C:/pdlf/app-factory/phase-e-build-and-verify/e38-config.md).

#### Step 38A: Package check

**Status:** Built.

**Files:** in `app-factory/phase-e-build-and-verify/`: `e38a-build-plan.md`, `e38a-test-spec.md`, `e38a-config.md`, `e38a-reference.md`, `e38a-explainer.md`, `e38a-decision-tree.html`, `e38a-module.md` (empty until the step is packaged).

**What it does and produces:** [[[pdlf:app-factory/phase-e-build-and-verify/e38a-explainer|Step 38A Explainer]]](C:/pdlf/app-factory/phase-e-build-and-verify/e38a-explainer.md); [[[pdlf:app-factory/phase-e-build-and-verify/e38a-config|Step 38A Configuration]]](C:/pdlf/app-factory/phase-e-build-and-verify/e38a-config.md).

#### Step 39: Triage

**Status:** Built.

**Files:** in `app-factory/phase-e-build-and-verify/`: `e39-build-plan.md`, `e39-test-spec.md`, `e39-config.md`, `e39-reference.md`, `e39-explainer.md`, `e39-decision-tree.html`, `e39-module.md` (empty until the step is packaged).

**What it does and produces:** [[[pdlf:app-factory/phase-e-build-and-verify/e39-explainer|Step 39 Explainer]]](C:/pdlf/app-factory/phase-e-build-and-verify/e39-explainer.md); [[[pdlf:app-factory/phase-e-build-and-verify/e39-config|Step 39 Configuration]]](C:/pdlf/app-factory/phase-e-build-and-verify/e39-config.md).

### Phase F — Ship and Monitor

#### Steps 41 to 46: Release readiness, Release to App 2, Release regression test, Client instance check, Release, Production check, Learning

**Files:** `app-factory/phase-f-ship-and-monitor/f41-*` to `f46-*`

**Status:** Step entries aligned to the release image of `spec-client-instance-hosting` (2026-11-08). References and configurations hold their first drafts. Each step is rebuilt at A1 when Phase F is reached.

### Phase G — Remaining apps

**File:** none.

**Status:** Not yet designed.
