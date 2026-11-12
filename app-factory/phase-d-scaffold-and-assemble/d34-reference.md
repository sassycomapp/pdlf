---
title: "d34-reference"
doc-id: "mb-b9f09cb4"
updated: "2026-11-12"
---
# Step 34 — Architecture Audit: Reference

What the agent does at Step 34, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d34-config|Step 34 Configuration]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d34-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2). The gate ceremony is in [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md) and is not repeated here.

## 1. Start

1. Read the entry record and Step 33's ledger row. Check Step 33 is complete for this run (test PR-01). If not: stop and raise a deviation.
2. Carry forward every input notice of Steps 31 to 33 to this step's receipt.
3. Read every input in the configuration.

## 2. The audit

4. Run every check in the configuration except Receipts, in order, with the skill each names. Write each check, its evidence and each finding into the audit report.
5. Handle each fault as the fault handling table in the configuration sets out. For a fault in what PDLF built: correct it at its step with David, run that step's checks again, then run this check again. For a fault in existing code or an existing form: put it on the rework list with its ticket, and check that the disposition list marks its module or form rework or remove; if it does not, the fault blocks the gate and goes to David.
6. Write the verdict into the report once every check passes or every remaining fault is on the rework list.

## 3. Checks

7. Run the Receipts check (test PR-05). On a failure: present it to David and correct it at its source.
8. Record every test in the checks file, naming its evidence.
9. Run `mb-sentinel-review` for Step 34 at Very High scrutiny on the audit report and the rework list. On Flag or Escalate: stop and present it to David. Check the review's `triage_findings` row exists and no finding is open (test PR-04).

## 4. The gate

10. Run the Full BFT for the gate.
11. Present the gate summary block in the configuration. Ask David: "Proceed to the build loop? (yes/no)".
12. On no: record the blocker, set the step's `status` to `blocked`, stop.
13. On yes: give David the command that records his approval, `bash /mnt/c/mybizz/scripts/pdlf-gate.sh {slug} architecture-verified {run}`, and wait until he confirms it ran. Never run it and never write to the `gates` table. Read the `gates` row and check `architecture-verified` is passed for the run; if it is not, stop. Record PR-03 in the checks file.

## 5. The end

14. Complete the Step 34 `steps` row with the ledger values in the configuration, and write the Full BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
15. Explain what was done, that Phase D is closed and that the build loop begins at Step 35. Present the Step Receipt, stop, and ask David to run `/mb-close-out`.
