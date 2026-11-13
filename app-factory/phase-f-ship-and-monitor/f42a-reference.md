---
title: "f42a-reference"
doc-id: "mb-89d4dfcf"
updated: "2026-11-13"
---
# Step 42A — Release Regression: Reference

What the agent does at Step 42A, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-f-ship-and-monitor/f42a-config|Step 42A Configuration]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f42a-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2).

1. Read the entry record and the ledger row of Step 42 for this run. Check it is complete or skipped (test PR-01). If not: stop and raise a deviation.
2. Carry forward every input notice to this step's receipt, and read every input in the configuration.
3. For an App 5 run: record the step `skipped`, write the receipt, stop.
4. Hand David `mg-grant --path ~/.gstack --count 15` and wait until he confirms it ran ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2.8).
5. Run `/qa-only` on every feature's flows on the test client instance, as each role and signed out, in Chrome, Firefox and Safari.
6. Run the release part of the assessment plan with `security-audit-methodology`.
7. Write every finding. On a failure: give David the instructions to move the test client instance back to the previous release image; stop and raise a deviation.
8. Record every test in the checks file, naming its evidence.
9. Run the Light BFT. Complete the Step 42A `steps` row with the ledger values in the configuration, and write the BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
10. Explain what was done. Present the Step Receipt, stop, and ask David to run `/mb-close-out`.
