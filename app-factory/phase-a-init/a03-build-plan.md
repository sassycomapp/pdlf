---
title: "a03-build-plan"
doc-id: "mb-9d12b137"
updated: "2026-10-29"
---
# Step 3 — New application with context: Build Plan

## Step entry

### Phase A — Init

#### Step 3: Entry point `new-app-with-context`

**Must achieve:** a Mybizz business that already has material (apps, documents, a reference platform) but has not run through PDLF, entered with that material named: which apps exist, where the project context is and which reference platform it follows, so that Step 11 sets it up around what exists and Step 12 reads the context.

**Starts from:** the business folder `C:\dev\dev-{slug}\`; App 1, in which David opened OpenCode; the business's existing apps and project library; GBrain; David's answers; the values in [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md).

**Produces:** the entry-point `steps` row holding the entry record; the `projects` row; the checks file and the Step Receipt in `pdlf-outputs\a03\`, written by Step 11; the Light BFT record.

**Carried out by:** the orchestrator (Step 1), with David answering every question.

**Must be built so that:**
- it works on App 1, run `app1`, and its run follows the Application route of [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md), joining at Step 11, route B;
- no health check runs first: the business is not yet set up by PDLF, and Step 11 ends with the health check as its self-audit;
- it names the context instead of guessing it: the apps that exist, the project context `{slug}-project-context`, and the reference platform with where its material is kept;
- the context's documents are found with a GBrain search and confirmed by David, and listed on the Step Receipt Step 11 writes for this entry;
- moving the old project library to `{slug}-project-context` and placing a reference platform's material are Step 11's, with David's permission;
- it writes the entry record into the `inputs_used` of its own `steps` row, with the fields of [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md), so every step of the run reads how the run began from one place;
- it changes nothing in the business's folders: it records, and the steps it joins act.

**BFT level:** Light, because the entry record shapes the whole run.

**References:** [[[pdlf:app-factory/phase-a-init/a01-reference|Step 1 Reference]]](C:/pdlf/app-factory/phase-a-init/a01-reference.md); [[[pdlf:app-factory/pdlf-build-plan|PDLF Build Plan]]](C:/pdlf/app-factory/pdlf-build-plan.md), section 4.

**Skills.** Every skill's output is used by the step named after the arrow.
- GBrain search: the context's documents, listed for David to confirm → Steps 11 and 12.

**Layers with no skill:** every layer of the application: an entry point builds nothing.

**Testing:** [[[pdlf:app-factory/phase-a-init/a03-test-spec|Step 3 Test Specification]]](C:/pdlf/app-factory/phase-a-init/a03-test-spec.md).

**Standards:** [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md): the app this entry works on.

## Why it is built this way

- **The context named at the entry.** Step 11 sets the business up around what exists, and Step 12 redevelops the application around its context. Both read the same answers from the entry record, so neither has to ask again or guess.
- **Nothing moved at the entry.** An entry point only records; every change to the business is made by Step 11, where it is checked and recorded.
- **The entry record in the entry's own row.** Every step of the run reads it from one place, and the entry is itself a step that is checked and recorded.
