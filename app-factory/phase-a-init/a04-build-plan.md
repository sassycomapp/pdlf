---
title: "a04-build-plan"
doc-id: "mb-cb089222"
updated: "2026-10-29"
---
# Step 4 — Feature for App 1: Build Plan

## Step entry

### Phase A — Init

#### Step 4: Entry point `add-feature-main-app`

**Must achieve:** a new feature for App 1 entered into PDLF with its statement and its own short name, after the business is shown healthy, so that Step 12 describes the feature against the application's approved design without re-scoping the application.

**Starts from:** the business folder; App 1, in which David opened OpenCode; the business's `projects` row and its application run `app1`; David's answers; the values in [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md).

**Produces:** the entry-point `steps` row holding the entry record; the health check report; the baseline suite results; the checks file and the Step Receipt in `pdlf-outputs\a04\`; the Light BFT record.

**Carried out by:** the orchestrator (Step 1), with David answering every question.

**Must be built so that:**
- it works on App 1, run the feature slug, and its run follows the Feature route of [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md), joining at Step 12, route C;
- the business's health check, [[[pdlf:pdlf-library/operating-procedures/sop-health-check|SOP: Health Check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md), passes first, before any other work, and its report is saved;
- the feature is described in David's words and named by a short name that is unique in the business and never `app{n}`, so its runs of Steps 12 to 16 never overwrite the application's;
- it runs only for an application whose run `app1` has passed `domain-locked`;
- App 1's whole test suite runs once before the feature starts, so a later failure can be told apart from one that already existed;
- it writes the entry record into the `inputs_used` of its own `steps` row, with the fields of [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md), so every step of the run reads how the run began from one place;
- it changes nothing in the business's folders: it records, and the steps it joins act.

**BFT level:** Light, because the entry record shapes the whole run.

**References:** [[[pdlf:app-factory/phase-a-init/a01-reference|Step 1 Reference]]](C:/pdlf/app-factory/phase-a-init/a01-reference.md); [[[pdlf:app-factory/pdlf-build-plan|PDLF Build Plan]]](C:/pdlf/app-factory/pdlf-build-plan.md), section 4.

**Skills.** Every skill's output is used by the step named after the arrow.
- None. The orchestrator asks David the questions and writes the entry record → Step 12, route C.

**Layers with no skill:** every layer of the application: an entry point builds nothing.

**Testing:** [[[pdlf:app-factory/phase-a-init/a04-test-spec|Step 4 Test Specification]]](C:/pdlf/app-factory/phase-a-init/a04-test-spec.md).

**Standards:** [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md): the app this entry works on.

## Why it is built this way

- **A feature, not a new application.** The application is already defined; the feature path describes only the feature, against the approved design.
- **A baseline first.** A failure found after the feature is built is only the feature's if the suite passed before it.
- **The entry record in the entry's own row.** Every step of the run reads it from one place, and the entry is itself a step that is checked and recorded.
