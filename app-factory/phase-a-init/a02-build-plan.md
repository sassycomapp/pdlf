---
title: "a02-build-plan"
doc-id: "mb-4e1a723a"
updated: "2026-10-29"
---
# Step 2 — New application, no context: Build Plan

## Step entry

### Phase A — Init

#### Step 2: Entry point `new-app-no-context`

**Must achieve:** a new Mybizz business, with no earlier material, entered into PDLF: its business row and its entry record written, so that Step 11 can set the business up from the project template.

**Starts from:** the business folder `C:\dev\dev-{slug}\`, holding only the empty App 1 repository, in which David opened OpenCode; David's answers; the values in [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md).

**Produces:** the entry-point `steps` row holding the entry record; the `projects` row; the checks file and the Step Receipt in `pdlf-outputs\a02\`, written by Step 11; the Light BFT record.

**Carried out by:** the orchestrator (Step 1), with David answering every question.

**Must be built so that:**
- it works on App 1, run `app1`, and its run follows the Application route of [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md), joining at Step 11, route A;
- no health check runs first: the business is not yet set up by PDLF, and Step 11 ends with the health check as its self-audit;
- it is taken only when the business folder holds nothing but the empty App 1 repository, because a business that already holds material is an application with context (entry 03);
- it asks only for the business's name and the mode: the slug is the App 1 repository's name without `-app1`, and Step 11 asks for the domain;
- it writes the entry record into the `inputs_used` of its own `steps` row, with the fields of [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md), so every step of the run reads how the run began from one place;
- it changes nothing in the business's folders: it records, and the steps it joins act.

**BFT level:** Light, because the entry record shapes the whole run.

**References:** [[[pdlf:app-factory/phase-a-init/a01-reference|Step 1 Reference]]](C:/pdlf/app-factory/phase-a-init/a01-reference.md); [[[pdlf:app-factory/pdlf-build-plan|PDLF Build Plan]]](C:/pdlf/app-factory/pdlf-build-plan.md), section 4.

**Skills.** Every skill's output is used by the step named after the arrow.
- None. The orchestrator asks David the questions and writes the entry record → Step 11, route A.

**Layers with no skill:** every layer of the application: an entry point builds nothing.

**Testing:** [[[pdlf:app-factory/phase-a-init/a02-test-spec|Step 2 Test Specification]]](C:/pdlf/app-factory/phase-a-init/a02-test-spec.md).

**Standards:** [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md): the app this entry works on.

## Why it is built this way

- **An empty folder only.** Material already in the folder is context, and context is entry 03's to read; taking entry 02 there would set it aside unread.
- **The entry record in the entry's own row.** Every step of the run reads it from one place, and the entry is itself a step that is checked and recorded.
