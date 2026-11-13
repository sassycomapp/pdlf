---
title: "f42-reference"
doc-id: "mb-8ad89930"
updated: "2026-11-13"
---
# Step 42 — Release to App 2: Reference

What the agent does at Step 42, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-f-ship-and-monitor/f42-config|Step 42 Configuration]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f42-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2).

1. Read the entry record and the ledger row of Step 41 for this run. Check it is complete or skipped (test PR-01). If not: stop and raise a deviation.
2. Carry forward every input notice to this step's receipt, and read every input in the configuration.
3. For an App 5 run: record the step `skipped`, write the receipt, stop.
4. For each item of the order of work in the configuration: give David its instructions, written with `wizard`; wait until he confirms; run its check. On a failed check: stop and raise a deviation; for a failure after item 6, give David the rollback instructions.
5. Write the image record. Record every test in the checks file, naming its evidence.
6. Run the Light BFT. Complete the Step 42 `steps` row with the ledger values in the configuration, and write the BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
7. Explain what was done. Present the Step Receipt, stop, and ask David to run `/mb-close-out`.
