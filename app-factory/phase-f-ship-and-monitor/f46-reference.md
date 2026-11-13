---
title: "f46-reference"
doc-id: "mb-2630906c"
updated: "2026-11-13"
---
# Step 46 — Learning: Reference

What the agent does at Step 46, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-f-ship-and-monitor/f46-config|Step 46 Configuration]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f46-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2). The gate ceremony is in [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md) and is not repeated here.

1. Read the entry record and the ledger row of Step 45 for this run. Check it is complete or skipped (test PR-01). If not: stop and raise a deviation.
2. Carry forward every input notice to this step's receipt, and read every input in the configuration.
3. Hand David `mg-grant --path ~/.gstack --count 15` and wait until he confirms it ran ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2.8).
4. Run `/retro` on the build's history, and `/learn` to export what GStack's skills learned.
5. Sort each lesson by the table in the configuration. Present each to David with where it goes; write each approved lesson into its source, and add a test where it fixes a problem.
6. Submit each written lesson to GBrain with `mb-submit-memory`.
7. Write the retrospective. Record every test in the checks file, naming its evidence.
8. Run the Full BFT for the gate. Present the gate summary block. Ask David: "Close this build cycle? (yes/no)".
9. On no: record the blocker, set the step's `status` to `blocked`, stop.
10. On yes: give David the command, `bash /mnt/c/mybizz/scripts/pdlf-gate.sh {slug} released {run}`, and wait until he confirms it ran. Never run it and never write to the `gates` table. Read the `gates` row; if it is not passed, stop. Record PR-03.
11. Complete the Step 46 `steps` row with the ledger values in the configuration, and write the Full BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
12. Explain what was done and that the build cycle is closed. Present the Step Receipt, stop, and ask David to run `/mb-close-out`.
