---
title: "c26-reference"
doc-id: "mb-16a8e604"
updated: "2026-11-12"
---
# Step 26 — Screens Approved: Reference

What the agent does at Step 26, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-c-design-and-plan/c26-config|Step 26 Configuration]]](C:/pdlf/app-factory/phase-c-design-and-plan/c26-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2). The gate ceremony is in [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md) and is not repeated here.

## 1. Start

1. Read the entry record and Step 23's ledger row. Check Step 23 is complete for this run (test PR-01). If not: stop and raise a deviation.
2. Carry forward every input notice of Steps 22 and 23 to this step's receipt.
3. Read every input in the configuration.

## 2. The findings

4. Correct every theme-usage finding and every other high finding in its screen requirement, or in `DESIGN.md`.
5. For each medium or low finding: show David the finding and its proposed correction, with your recommendation. Correct it, or record it as declined with David's reason.
6. Write each finding's outcome to the finding outcomes file.
7. Check every screen requirement against test DC-16 again. On a failure: correct it and check again.

## 3. Approval

8. Present each screen requirement to David, in the tickets' build order. Correct each change he asks for, and present it again until he approves it. Set its front matter to `status: approved`.
9. Copy each approved requirement into the step folder.

## 4. Checks

10. Run `ts_report.py` with `--check` on the receipts of Steps 21 to 23 of the run (test PR-05). On a failure: present it to David and correct it at its source.
11. Record DC-16 and PR-05 in the checks file.

## 5. The gate

12. Check that no finding is open and every screen requirement is approved. If not: return to section 2 or 3. Never offer the gate before.
13. Run the Full BFT for the gate.
14. Present the gate summary block in the configuration. Ask David: "Proceed to Phase D? (yes/no)".
15. On no: record the blocker, set the step's `status` to `blocked`, stop.
16. On yes: give David the command that records his approval, `bash /mnt/c/mybizz/scripts/pdlf-gate.sh {slug} screens-approved {run}`, and wait until he confirms it ran. Never run it and never write to the `gates` table. Read the `gates` row and check `screens-approved` is passed for the run; if it is not, stop. Record PR-03 in the checks file.

## 6. The end

17. Complete the Step 26 `steps` row with the ledger values in the configuration, and write the Full BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
18. Explain what was done, that Phase C is closed and Phase D begins. Present the Step Receipt, stop, and ask David to run `/mb-close-out`.
