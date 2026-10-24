---
title: "c21-build-plan"
doc-id: "mb-00f53c9a"
updated: "2026-10-24"
---

## From `pdlf-build-plan.md`: step entry

### Phase C — Design and Plan

Ends with the gates `concept-locked` (Step 21) and `wireframes-approved` (Step 26).

#### Step 21: Concept sanity audit

**Must achieve:** Cross-checks everything produced so far for contradictions and reports the verdict.

**Carried out by:** OpenCode.

**Gate:** `concept-locked`: the concept is locked; no new feature without reopening the gate.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

**Skills.** No installed skill cross-checks documents for contradictions, so OpenCode does this step.
- `mb-sentinel-review`, Medium → `triage_findings`.

**Inputs:** the CEO plan, the reviewed plan and test plan, the threat model, `GLOSSARY.md` and the ADRs, the tickets and flows from Step 19, and `DESIGN.md`.

**Testing:** every pair of inputs is checked, and the report names each pair checked → the developer at the gate.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to cross-artifact consistency
2. Read all Phase B+C outputs — CEO review (Step 14), Eng review (Step 15), GLOSSARY.md + ADRs (Step 16), DESIGN.md (Step 20)
3. Cross-reference each document pair for contradictions
4. Produce audit report — What was checked, findings, discrepancies, verdict
5. Save audit report — `<project-library>/pdlf/step-21-concept-audit.md`
6. Execute gate procedure — per `specifications-local/spec-gate-procedure.md`
7. Gate: `concept-locked` — Full BFT, gate summary, developer approval required; no new feature without formal gate reopening
8. Write Step 21 ledger row — `completed_at`
9. Generate Step Receipt — `<project-library>/pdlf/outputs/step-21-receipt.md`
10. Apply BFT — Full (gate override)
11. Follow execution sequence — Housekeeping, stop, wait for continue
