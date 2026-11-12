---
title: "c26-build-plan"
doc-id: "mb-220a58b2"
updated: "2026-11-12"
---
# Step 26 — Screens Approved: Build Plan

## Step entry

### Phase C — Design and Plan

Ends with the gates `concept-locked` (Step 21) and `screens-approved` (this step).

#### Step 26: Screens approved

**Must achieve:** every finding of Step 23 corrected or declined by David, every screen requirement approved by David, and the screens locked at the gate `screens-approved`, so that `mb-form-builder` builds each form from an approved design; Phase C closed.

**Starts from:** the screen requirements and the requirement index from Step 22; the design review from Step 23; `DESIGN.md`; the Step Receipts of Steps 17 to 23.

**Produces:** every screen requirement corrected and set to `status: approved`; `DESIGN.md` corrected where a finding concerns it; the record of each finding's outcome; the `gates` row of `screens-approved`; in `pdlf-outputs\c26\`: the copies, the test results and the Step Receipt; the ledger row and the BFT record.

**Carried out by:** OpenCode. David decides each finding he is asked about, approves each screen requirement and passes or blocks the gate.

**Must be built so that:**
- every high finding is corrected in its screen requirement; every medium or low finding is corrected, or declined by David with his reason;
- a theme-usage finding is never declined: the better-fitting component replaces the plainer one;
- after the corrections, every screen requirement passes test DC-16 again;
- David approves each screen requirement; the agent then sets its front matter to `status: approved`;
- the gate is not offered while any finding is open or any screen requirement is not approved;
- before the gate, the receipts of Steps 21 to 23 of the run match their evidence (test PR-05);
- the gate follows `spec-gate-procedure`: Full BFT, the gate summary block, and David's explicit yes or no; on yes David records his approval with `pdlf-gate.sh`, which writes the `gates` row, and the agent reads the row; the agent never writes it;
- after the gate, a screen requirement changes only through a deviation David authorises;
- it hands to Phase D the approved screen requirements, the requirement index, the access matrix, `DESIGN.md` and the tickets; the forms themselves are built feature by feature by `mb-form-builder`, after each feature's server code;
- its ledger row is `step_type = 'gate'`, `skill_family = 'opencode'`, `synthesized = false`, `run` and `app_number` from the entry record, and `inputs_used` naming Steps 22 and 23.

**BFT level:** Full (gate).

**Gate:** `screens-approved`: every screen requirement is approved and locked; Phase C is closed.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md), [[[default:specifications-global/mo-ui-production|UI Production Method]]](C:/dev/project-library-global/specifications-global/mo-ui-production.md), [[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md).

**Skills.** None. OpenCode corrects the requirements from the findings; David approves.

**Layers with no skill:** all; the step corrects and approves documents.

**Testing:** [[[pdlf:app-factory/phase-c-design-and-plan/c26-test-spec|Step 26 Test Specification]]](C:/pdlf/app-factory/phase-c-design-and-plan/c26-test-spec.md): every finding is closed, every screen requirement passes DC-16 and is approved, and the gate has David's approval.

**Standards:** [[[default:specifications-global/spec-ui-standards|UI Standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md).

## Why it is built this way

- **Approved design, then build.** `mb-form-builder` builds only from an approved screen requirement, so this gate is the point at which every form's design becomes fixed.
- **No plain component survives.** A theme-usage finding cannot be declined, so every approved screen uses the best component the theme has.
- **David approves each screen.** Each requirement is approved on its own, so no screen is approved by being part of a batch.
