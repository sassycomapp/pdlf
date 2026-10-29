---
title: "a08-build-plan"
doc-id: "mb-b38b9010"
updated: "2026-10-29"
---
# Step 8 — Create App 5: Build Plan

## Step entry

### Phase A — Init

#### Step 8: Entry point `create-management-app`

**Must achieve:** App 5, the management app, entered into PDLF for a business whose existing apps are shown healthy, so that Step 11 sets it up and Steps 12 to 16 design it: it receives every client instance's heartbeat, flags clients that need a higher plan tier, and runs each client's exit handover.

**Starts from:** the business folder, in which David opened OpenCode; the business's `projects` row and App 1's approved design doc; David's answers; the values in [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md).

**Produces:** the entry-point `steps` row holding the entry record; the health check report; the checks file and the Step Receipt in `pdlf-outputs\a08\`; the Light BFT record.

**Carried out by:** the orchestrator (Step 1), with David answering every question.

**Must be built so that:**
- it works on App 5, run `app5`, and its run follows the Management app route of [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md), joining at Step 11, route C;
- the business's health check, [[[pdlf:pdlf-library/operating-procedures/sop-health-check|SOP: Health Check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md), passes first, before any other work, and its report is saved;
- App 5 is designed by Steps 12 to 16 from App 1's approved design doc and its role in the five-app structure: it receives every client instance's heartbeat, flags clients that need a higher plan tier, and runs the client exit handover of [[[default:adr-global/adr-client-r2-storage-and-exit-handover|Client R2 Storage and Exit Handover]]](C:/dev/project-library-global/adr-global/adr-client-r2-storage-and-exit-handover.md);
- it writes the entry record into the `inputs_used` of its own `steps` row, with the fields of [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md), so every step of the run reads how the run began from one place;
- it changes nothing in the business's folders: it records, and the steps it joins act.

**BFT level:** Light, because the entry record shapes the whole run.

**References:** [[[pdlf:app-factory/phase-a-init/a01-reference|Step 1 Reference]]](C:/pdlf/app-factory/phase-a-init/a01-reference.md); [[[pdlf:app-factory/pdlf-build-plan|PDLF Build Plan]]](C:/pdlf/app-factory/pdlf-build-plan.md), section 4.

**Skills.** Every skill's output is used by the step named after the arrow.
- None. The orchestrator asks David the questions and writes the entry record → Step 11, route C.

**Layers with no skill:** every layer of the application: an entry point builds nothing.

**Testing:** [[[pdlf:app-factory/phase-a-init/a08-test-spec|Step 8 Test Specification]]](C:/pdlf/app-factory/phase-a-init/a08-test-spec.md).

**Standards:** [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md): the app this entry works on.

## Why it is built this way

- **Designed, unlike App 3.** App 5 is an application of its own, with its own users and work, so it runs through the design steps.
- **The entry record in the entry's own row.** Every step of the run reads it from one place, and the entry is itself a step that is checked and recorded.
