---
title: "c21-reference"
doc-id: "mb-06a9bf5e"
updated: "2026-11-12"
---
# Step 21 — Concept Check: Reference

What the agent does at Step 21, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-c-design-and-plan/c21-config|Step 21 Configuration]]](C:/pdlf/app-factory/phase-c-design-and-plan/c21-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2). The gate ceremony is in [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md) and is not repeated here.

## 1. Start

1. Read the entry record and Step 20's ledger row. Check Step 20 is complete or skipped for this run (test PR-01). If not: stop and raise a deviation.
2. Carry forward every input notice of Steps 17 to 20 to this step's receipt.
3. Read every concept document in the configuration, in full.

## 2. The check

4. Check every pair of concept documents for contradictions, and run every fixed check in the configuration except Receipts. Write each pair, what was compared and each contradiction into the concept check report.
5. For each contradiction: show David the two statements and your recommended correction. Correct the source document with his decision, then check the pair again.
6. Write the verdict into the report once no contradiction remains.

## 3. Checks

7. Run the Receipts check in the configuration (test PR-05). On a failure: present it to David and correct it at its source.
8. Record DC-11 and PR-05 in the checks file.
9. Run `mb-sentinel-review` for Step 21 at Medium scrutiny on the report. On Flag or Escalate: stop and present it to David. Check the review's `triage_findings` row exists (test PR-04).

## 4. The gate

10. Run the Full BFT for the gate.
11. Present the gate summary block in the configuration. Ask David: "Proceed to the screen requirements? (yes/no)".
12. On no: record the blocker, set the step's `status` to `blocked`, stop.
13. On yes: give David the command that records his approval, `bash /mnt/c/mybizz/scripts/pdlf-gate.sh {slug} concept-locked {run}`, and wait until he confirms it ran. Never run it and never write to the `gates` table. Read the `gates` row and check `concept-locked` is passed for the run; if it is not, stop. Record PR-03 in the checks file.

## 5. The end

14. Complete the Step 21 `steps` row with the ledger values in the configuration, and write the Full BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
15. Explain what was done and that the concept is locked. Present the Step Receipt, stop, and ask David to run `/mb-close-out`.
