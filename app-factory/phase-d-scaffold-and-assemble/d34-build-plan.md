---
title: "d34-build-plan"
doc-id: "mb-08fb22cb"
updated: "2026-10-22"
---

## From `pdlf-build-plan.md`: step entry

### Phase D — Scaffold and Assemble

Ends with the gate `architecture-verified` (Step 34).

#### Step 34: Architectural sanity audit

**Must achieve:** Checks the tables, forms and scaffold against the locked decisions, so that nothing has drifted before any code is written.

**Carried out by:** OpenCode.

**Gate:** `architecture-verified`: the structure is verified and coding may begin.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `graphify`: builds the code graph of the scaffold → the comparison with `scaffold-plan.md` and Step 15's architecture diagram, then Steps 35 and 40.
- `data-models` (Anvil): checks the tables, model classes and client access against the data design → the audit report.
- `secure-software-engineering` (Magnus919): verifies the skeleton against Step 15's list of trust boundaries → the audit report.
- `security-audit-methodology` (Magnus919): runs the architecture part of Step 15's security assessment plan → the audit report.
- `mb-sentinel-review`, Very High → `triage_findings`; an open finding blocks the gate.
- `anvil --json validate .` over the whole app → the audit report.

**Testing:** the whole app validates; every table, form and stub traces to a locked decision.

**Must be built so that:**
- the audit checks the skeleton against [[[default:policy-global/pol-common-aspects-for-mybizz-anvil-applications|Common Aspects for Mybizz Anvil Applications]]](C:/dev/project-library-global/policy-global/pol-common-aspects-for-mybizz-anvil-applications.md) and confirms the client instance needs no code of its own;

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to architecture verification
2. Compare actual Anvil data tables against ADRs and domain model — Every table/column traces to a locked decision
3. Compare actual UI forms against approved screens and DESIGN.md
4. Compare actual scaffolding against `scaffold-plan.md` — Every planned module/function exists, nothing improvised
5. Check for drift — If found, correct Anvil-side artifact or formally update plan/ADR per deviation mechanism
6. Produce audit report — What was checked, findings, discrepancies, verdict
7. Save audit report — `<project-library>/pdlf/step-34-architecture-audit.md`
8. Execute gate procedure — per `specifications-local/spec-gate-procedure.md`
9. Gate: `architecture-verified` — Full BFT, gate summary, developer approval required before any code-writing begins
10. Write Step 34 ledger row — `completed_at`
11. Generate Step Receipt — `<project-library>/pdlf/outputs/step-34-receipt.md`
12. Apply BFT — Full (gate override)
13. Follow execution sequence — Housekeeping, stop, wait for continue
