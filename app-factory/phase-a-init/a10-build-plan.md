---
title: "a10-build-plan"
doc-id: "mb-47feff2f"
updated: "2026-10-29"
---
# Step 10 — Update to App 3 or App 5: Build Plan

## Step entry

### Phase A — Init

#### Step 10: Entry point `update-management-app`

**Must achieve:** an update to App 3 or App 5 entered into PDLF, after the business is shown healthy, as a feature when it changes what the app does and otherwise at the step David names, with the root cause of a fault found first.

**Starts from:** the business folder, in which David opened OpenCode; the business's `projects` row and the app's run `app{n}`; David's answers; the values in [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md).

**Produces:** the entry-point `steps` row holding the entry record; the health check report; the baseline suite results; the diagnosis, when the update corrects a fault; the checks file and the Step Receipt in `pdlf-outputs\a10\`; the Light BFT record.

**Carried out by:** the orchestrator (Step 1), with David answering every question.

**Must be built so that:**
- it works on App 3 or 5, run the update slug, and its run follows the Feature, when the update changes what the app does; otherwise Update route of [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md), joining at Step 12 for a Feature run; otherwise the step David names;
- the business's health check, [[[pdlf:pdlf-library/operating-procedures/sop-health-check|SOP: Health Check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md), passes first, before any other work, and its report is saved;
- an update that changes what the app does is a feature; any other update starts at the step David names;
- a fault's root cause is found with `diagnosing-bugs` before the work starts;
- App 5's whole suite runs once before the update starts; App 3 holds no code;
- it writes the entry record into the `inputs_used` of its own `steps` row, with the fields of [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md), so every step of the run reads how the run began from one place;
- it changes nothing in the business's folders: it records, and the steps it joins act.

**BFT level:** Light, because the entry record shapes the whole run.

**References:** [[[pdlf:app-factory/phase-a-init/a01-reference|Step 1 Reference]]](C:/pdlf/app-factory/phase-a-init/a01-reference.md); [[[pdlf:app-factory/pdlf-build-plan|PDLF Build Plan]]](C:/pdlf/app-factory/pdlf-build-plan.md), section 4.

**Skills.** Every skill's output is used by the step named after the arrow.
- `diagnosing-bugs` (Matt Pocock): when the update corrects a fault, the root cause → the step David names.

**Layers with no skill:** every layer of the application: an entry point builds nothing.

**Testing:** [[[pdlf:app-factory/phase-a-init/a10-test-spec|Step 10 Test Specification]]](C:/pdlf/app-factory/phase-a-init/a10-test-spec.md).

**Standards:** [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md): the app this entry works on.

## Why it is built this way

- **A change of behaviour is a feature.** It needs describing and reviewing; a correction goes straight to the step that makes it.
- **The root cause first.** A fix made before the cause is found treats the symptom.
- **The entry record in the entry's own row.** Every step of the run reads it from one place, and the entry is itself a step that is checked and recorded.
