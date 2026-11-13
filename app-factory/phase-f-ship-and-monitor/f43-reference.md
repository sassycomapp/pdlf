---
title: "f43-reference"
doc-id: "mb-6e45109d"
updated: "2026-11-13"
---
# Step 43 — Client Instance Check: Reference

What the agent does at Step 43, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-f-ship-and-monitor/f43-config|Step 43 Configuration]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f43-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2).

1. Read the entry record and the ledger row of Step 42A for this run. Check it is complete or skipped (test PR-01). If not: stop and raise a deviation.
2. Carry forward every input notice to this step's receipt, and read every input in the configuration.
3. For an App 5 run: record the step `skipped`, write the receipt, stop.
4. Hand David `mg-grant --path ~/.gstack --count 15` and wait until he confirms it ran ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2.8).
5. Check the heartbeat reports the release version and schema fingerprint. Run the quick smoke test with `/qa-only`.
6. Record the health baseline with `/canary`.
7. Run SC-14, and at a first release RL-10.
8. On a failure: give David the rollback instructions; stop and raise a deviation.
9. Record every test in the checks file, naming its evidence.
10. Run the Light BFT. Complete the Step 43 `steps` row with the ledger values in the configuration, and write the BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
11. Explain what was done. Present the Step Receipt, stop, and ask David to run `/mb-close-out`.
