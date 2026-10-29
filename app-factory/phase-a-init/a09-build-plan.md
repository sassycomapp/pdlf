---
title: "a09-build-plan"
doc-id: "mb-690664f0"
updated: "2026-10-29"
---
# Step 9 — Feature for App 3 or App 5: Build Plan

## Step entry

### Phase A — Init

#### Step 9: Entry point `add-feature-management-app`

**Must achieve:** a new feature for App 3 or App 5 entered into PDLF with its statement and its own short name, after the business is shown healthy, so that Step 12 describes it against that app's approved design.

**Starts from:** the business folder, in which David opened OpenCode; the business's `projects` row and the app's run `app{n}`; David's answers; the values in [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md).

**Produces:** the entry-point `steps` row holding the entry record; the health check report; the baseline suite results; the checks file and the Step Receipt in `pdlf-outputs\a09\`; the Light BFT record.

**Carried out by:** the orchestrator (Step 1), with David answering every question.

**Must be built so that:**
- it works on App 3 or 5, run the feature slug, and its run follows the Feature route of [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md), joining at Step 12, route C;
- the business's health check, [[[pdlf:pdlf-library/operating-procedures/sop-health-check|SOP: Health Check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md), passes first, before any other work, and its report is saved;
- the feature belongs to App 3 or App 5, named by a short name unique in the business;
- App 5's whole suite runs once before the feature starts; App 3 holds no code;
- it writes the entry record into the `inputs_used` of its own `steps` row, with the fields of [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md), so every step of the run reads how the run began from one place;
- it changes nothing in the business's folders: it records, and the steps it joins act.

**BFT level:** Light, because the entry record shapes the whole run.

**References:** [[[pdlf:app-factory/phase-a-init/a01-reference|Step 1 Reference]]](C:/pdlf/app-factory/phase-a-init/a01-reference.md); [[[pdlf:app-factory/pdlf-build-plan|PDLF Build Plan]]](C:/pdlf/app-factory/pdlf-build-plan.md), section 4.

**Skills.** Every skill's output is used by the step named after the arrow.
- None. The orchestrator asks David the questions and writes the entry record → Step 12, route C.

**Layers with no skill:** every layer of the application: an entry point builds nothing.

**Testing:** [[[pdlf:app-factory/phase-a-init/a09-test-spec|Step 9 Test Specification]]](C:/pdlf/app-factory/phase-a-init/a09-test-spec.md).

**Standards:** [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md): the app this entry works on.

## Why it is built this way

- **The same feature path for every app.** A feature is described, reviewed and modelled the same way whichever app it belongs to.
- **The entry record in the entry's own row.** Every step of the run reads it from one place, and the entry is itself a step that is checked and recorded.
