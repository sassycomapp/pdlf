---
title: "a07-build-plan"
doc-id: "mb-b0915c10"
updated: "2026-10-29"
---
# Step 7 — Create App 3: Build Plan

## Step entry

### Phase A — Init

#### Step 7: Entry point `create-client-template`

**Must achieve:** App 3, `blank_client_template`, entered into PDLF for a business whose existing apps are shown healthy, so that Step 11 sets it up; Steps 12 to 16 do not run for it, because it holds only App 1's schema, one startup module and its dependency on App 2.

**Starts from:** the business folder, in which David opened OpenCode; the business's `projects` row; David's answers; the values in [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md).

**Produces:** the entry-point `steps` row holding the entry record; the health check report; the checks file and the Step Receipt in `pdlf-outputs\a07\`; the Light BFT record.

**Carried out by:** the orchestrator (Step 1), with David answering every question.

**Must be built so that:**
- it works on App 3, run `app3`, and its run follows the Client template route of [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md), joining at Step 11, route C;
- the business's health check, [[[pdlf:pdlf-library/operating-procedures/sop-health-check|SOP: Health Check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md), passes first, before any other work, and its report is saved;
- Steps 12 to 16 never run for App 3, because it has nothing to design;
- it writes the entry record into the `inputs_used` of its own `steps` row, with the fields of [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md), so every step of the run reads how the run began from one place;
- it changes nothing in the business's folders: it records, and the steps it joins act.

**BFT level:** Light, because the entry record shapes the whole run.

**References:** [[[pdlf:app-factory/phase-a-init/a01-reference|Step 1 Reference]]](C:/pdlf/app-factory/phase-a-init/a01-reference.md); [[[pdlf:app-factory/pdlf-build-plan|PDLF Build Plan]]](C:/pdlf/app-factory/pdlf-build-plan.md), section 4.

**Skills.** Every skill's output is used by the step named after the arrow.
- None. The orchestrator asks David the questions and writes the entry record → Step 11, route C.

**Layers with no skill:** every layer of the application: an entry point builds nothing.

**Testing:** [[[pdlf:app-factory/phase-a-init/a07-test-spec|Step 7 Test Specification]]](C:/pdlf/app-factory/phase-a-init/a07-test-spec.md).

**Standards:** [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md): the app this entry works on.

## Why it is built this way

- **No design steps.** App 3 is built from App 1's schema; there is nothing in it to scope or review.
- **The entry record in the entry's own row.** Every step of the run reads it from one place, and the entry is itself a step that is checked and recorded.
