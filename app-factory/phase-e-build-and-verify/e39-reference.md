---
title: "e39-reference"
doc-id: "mb-43a89cf2"
updated: "2026-11-13"
---
# Step 39 — Triage: Reference

What the agent does at Step 39, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-e-build-and-verify/e39-config|Step 39 Configuration]]](C:/pdlf/app-factory/phase-e-build-and-verify/e39-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2). The gate ceremony is in [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md) and is not repeated here.

## 1. Start

1. Read the entry record and the ledger row of Step 38A for this ticket. Check it is complete or skipped (test PR-01). If not: stop and raise a deviation.
2. Read the ticket, and every input in the configuration.

## 2. Triage

3. Run `triage` on every finding of Steps 35A to 38A for the ticket, with the label vocabulary. Write each label and decision to `triage_findings` and the triage record. Ask David to decide each finding the vocabulary does not settle.
4. For each finding labelled for a fix: return the feature to Step 35 as a deviation; there, `diagnosing-bugs` finds its root cause and a test is added. Then Steps 35A to 38A run again, and this step starts again.
5. Check every row of `triage_findings` for the ticket is resolved or `wontfix` with David's reason.

## 3. Checks

6. Run the whole suite (test PR-08). Run `ts_report.py --check` on the receipts of Steps 35 to 38A of the ticket (test PR-05). On a failure: correct it at its source.
7. Close the ticket and mark its rework items cleared.
8. Record every test in the checks file, naming its evidence.

## 4. The gate

9. Run the Full BFT for the gate.
10. Present the gate summary block in the configuration. Ask David: "Lock this feature and start the next? (yes/no)".
11. On no: record the blocker, set the step's `status` to `blocked`, stop.
12. On yes: give David the command that records his approval, `bash /mnt/c/mybizz/scripts/pdlf-gate.sh {slug} build-verified {run} {ticket}`, and wait until he confirms it ran. Never run it and never write to the `gates` table. Read the `gates` row and check `build-verified` is passed for the ticket; if it is not, stop. Record PR-03 in the checks file.

## 5. The end

13. Complete the Step 39 `steps` row with the ledger values in the configuration, and write the Full BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
14. Explain what was done, and name the next ticket, or Step 41 when every ticket has passed. Present the Step Receipt, stop, and ask David to run `/mb-close-out`.
