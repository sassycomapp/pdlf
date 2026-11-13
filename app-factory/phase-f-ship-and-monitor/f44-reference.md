---
title: "f44-reference"
doc-id: "mb-ac475804"
updated: "2026-11-13"
---
# Step 44 — Release: Reference

What the agent does at Step 44, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-f-ship-and-monitor/f44-config|Step 44 Configuration]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f44-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2). The gate ceremony is in [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md) and is not repeated here.

1. Read the entry record and the ledger row of Step 43 for this run. Check it is complete or skipped (test PR-01). If not: stop and raise a deviation.
2. Carry forward every input notice to this step's receipt, and read every input in the configuration.
3. Check `triage_findings` has no open finding for the run. If it has: stop and present them to David.
4. Run `ts_report.py --check` on the receipts of Steps 41 to 43 (test PR-05). On a failure: correct it at its source.
5. Run the Full BFT for the gate. Present the gate summary block. Ask David: "Release to every client? (yes/no)".
6. On no: record the blocker, set the step's `status` to `blocked`, stop.
7. On yes: give David the command that records his approval, `bash /mnt/c/mybizz/scripts/pdlf-gate.sh {slug} production-released {run}`, and wait until he confirms it ran. Never run it and never write to the `gates` table. Read the `gates` row; if it is not passed, stop. Record PR-03.
8. For App 1: give David the instructions to run App 5's Release action. Check each stage's health check in App 5 before the next. On a failed stage: confirm it rolled back, stop and raise a deviation.
9. For App 5: give David the instructions to publish App 5's tagged release in Anvil, and confirm the published version.
10. Write the release record. Record every test in the checks file, naming its evidence.
11. Complete the Step 44 `steps` row with the ledger values in the configuration, and write the Full BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
12. Explain what was done. Present the Step Receipt, stop, and ask David to run `/mb-close-out`.
