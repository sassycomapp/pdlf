---
title: "c20-reference"
doc-id: "mb-64d59065"
updated: "2026-11-12"
---
# Step 20 — Design System: Reference

What the agent does at Step 20, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-c-design-and-plan/c20-config|Step 20 Configuration]]](C:/pdlf/app-factory/phase-c-design-and-plan/c20-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2).

## 1. Start

1. Read the entry record and Step 19's ledger row. Check Step 19 is complete for this run (test PR-01). If not: stop and raise a deviation.
2. In a test run: offer David full, abbreviated or skipped, as `pol-step-conditional-state` sets out. On skip: record it and go to step 9.
3. Carry forward every input notice of Step 19 to this step's receipt. Read every input in the configuration, including the theme guide and the whole component inventory.

## 2. The design system

4. Start `/design-consultation` from the project library with the inputs and the fixed answers in the configuration. Hold it to the choices in the configuration.
5. Write `docs-local\DESIGN.md` with each choice and the fixed statements in the configuration. For an existing `DESIGN.md`: bring it to these rules and keep every choice David made that still meets them.
6. Present `DESIGN.md` to David. Correct each change he asks for, and present it again until he approves it.

## 3. Checks

7. Check the chosen palette against test DC-12 in light and dark mode, and record the result in the checks file.
8. Run `mb-sentinel-review` for Step 20 at Medium scrutiny on `DESIGN.md`. On Flag or Escalate: stop and present it to David. Check the review's `triage_findings` row exists (test PR-04). Copy `DESIGN.md` into the step folder.

## 4. The end

9. Run the Full BFT. Complete the Step 20 `steps` row with the ledger values in the configuration, and write the BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
10. Explain what was done. Present the Step Receipt, stop, and ask David to run `/mb-close-out`.
