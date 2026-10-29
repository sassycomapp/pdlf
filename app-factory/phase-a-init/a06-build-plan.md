---
title: "a06-build-plan"
doc-id: "mb-370e9733"
updated: "2026-10-29"
---
# Step 6 — Release into App 2: Build Plan

## Step entry

### Phase A — Init

#### Step 6: Entry point `compile-master-template`

**Must achieve:** a release of App 1's approved code into App 2, `master_template`, entered into PDLF after the business is shown healthy and App 1's suite passes, so that the release steps start from a sound App 1.

**Starts from:** the business folder, in which David opened OpenCode; the business's `projects` row; App 1; the values in [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md).

**Produces:** the entry-point `steps` row holding the entry record; the health check report; the baseline suite results; the checks file and the Step Receipt in `pdlf-outputs\a06\`; the Light BFT record.

**Carried out by:** the orchestrator (Step 1), with David answering every question.

**Must be built so that:**
- it works on App 2, run `app2`, and its run follows the Release route of [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md), joining at Step 41;
- the business's health check, [[[pdlf:pdlf-library/operating-procedures/sop-health-check|SOP: Health Check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md), passes first, before any other work, and its report is saved;
- the release starts only from an App 1 whose whole suite passes, because App 2 reaches every client at once;
- it writes the entry record into the `inputs_used` of its own `steps` row, with the fields of [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md), so every step of the run reads how the run began from one place;
- it changes nothing in the business's folders: it records, and the steps it joins act.

**BFT level:** Light, because the entry record shapes the whole run.

**References:** [[[pdlf:app-factory/phase-a-init/a01-reference|Step 1 Reference]]](C:/pdlf/app-factory/phase-a-init/a01-reference.md); [[[pdlf:app-factory/pdlf-build-plan|PDLF Build Plan]]](C:/pdlf/app-factory/pdlf-build-plan.md), section 4.

**Skills.** Every skill's output is used by the step named after the arrow.
- None. The orchestrator asks David the questions and writes the entry record → Step 41.

**Layers with no skill:** every layer of the application: an entry point builds nothing.

**Testing:** [[[pdlf:app-factory/phase-a-init/a06-test-spec|Step 6 Test Specification]]](C:/pdlf/app-factory/phase-a-init/a06-test-spec.md).

**Standards:** [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md): the app this entry works on.

## Why it is built this way

- **A passing App 1 only.** App 2 is the dependency of every client instance; a fault released into it reaches every client.
- **The entry record in the entry's own row.** Every step of the run reads it from one place, and the entry is itself a step that is checked and recorded.
