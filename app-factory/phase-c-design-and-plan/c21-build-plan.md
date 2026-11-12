---
title: "c21-build-plan"
doc-id: "mb-00f53c9a"
updated: "2026-11-12"
---
# Step 21 — Concept Check: Build Plan

## Step entry

### Phase C — Design and Plan

Ends with the gates `concept-locked` (this step) and `screens-approved` (Step 26).

#### Step 21: Concept check

**Must achieve:** every concept document checked against every other for contradictions, each contradiction resolved with David, and the concept locked by David at the gate `concept-locked`, so that no feature enters after the screens are designed.

**Starts from:** the reviewed plan, the test plan, the access matrix, the threat model, the glossary and the ADRs, handed over at Step 16; the authoritative schema from Step 17; the tickets and flows from Step 19; `DESIGN.md` from Step 20; the Step Receipts of Steps 17 to 20.

**Produces:** the concept check report; each contradiction corrected at its source; the `gates` row of `concept-locked`; in `pdlf-outputs\c21\`: the report, the test results and the Step Receipt; the ledger row, the BFT record and Sentinel's `triage_findings` row.

**Carried out by:** OpenCode and `mb-sentinel-review`. David resolves each contradiction and passes or blocks the gate.

**Must be built so that:**
- every pair of the concept documents is checked, and the report names each pair and what was compared;
- the checks include: every ticket's tables exist in the authoritative schema; every ticket's server functions and forms appear in the access matrix's roles, or are listed for Step 22 to add; every term in the tickets and `DESIGN.md` is the glossary's term; every ticket's tests exist in the test plan; every ADR is followed by the documents it governs;
- each contradiction is shown to David with the agent's recommended correction, and corrected at its source with his decision; the pair is then checked again;
- before the gate, the receipts of Steps 17 to 20 of the run match their evidence (test PR-05);
- the gate follows `spec-gate-procedure`: Full BFT, the gate summary block, and David's explicit yes or no; on yes David records his approval with `pdlf-gate.sh`, which writes the `gates` row, and the agent reads the row; the agent never writes it;
- after the gate, no feature is added without the gate being reopened by a deviation David authorises;
- its ledger row is `step_type = 'gate'`, `skill_family = 'opencode'`, `synthesized = false`, `run` and `app_number` from the entry record, and `inputs_used` naming Steps 16 to 20.

**BFT level:** Full (gate).

**Gate:** `concept-locked`: the concept is locked; no feature is added after it without the gate being reopened.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md), [[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md).

**Skills.** No installed skill checks documents against each other for contradictions, so OpenCode does it.
- `mb-sentinel-review`, Medium → `triage_findings`.

**Layers with no skill:** all but security; the step reads and compares.

**Testing:** [[[pdlf:app-factory/phase-c-design-and-plan/c21-test-spec|Step 21 Test Specification]]](C:/pdlf/app-factory/phase-c-design-and-plan/c21-test-spec.md): every pair was checked, every contradiction resolved, the receipts match their evidence, and the gate has David's approval.

**Standards:** the documents themselves; the glossary decides every term.

## Why it is built this way

- **Every pair.** A contradiction lives between two documents, so only a check of every pair finds them all.
- **Corrected at the source.** A contradiction fixed in the report and not in its document would return in the next step that reads it.
- **Locked before screens.** Screens are designed next; a feature added after that point would be designed without its place in the whole.
