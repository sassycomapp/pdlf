---
title: "e36-reference"
doc-id: "mb-60ebe004"
updated: "2026-11-13"
---
# Step 36 — Design Review: Reference

What the agent does at Step 36, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-e-build-and-verify/e36-config|Step 36 Configuration]]](C:/pdlf/app-factory/phase-e-build-and-verify/e36-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2).

1. Read the entry record and the ledger row of Step 40B for this ticket. Check it is complete or skipped (test PR-01). If not: stop and raise a deviation.
2. Read the ticket, and every input in the configuration.
3. Hand David `mg-grant --path ~/.gstack --count 15` and wait until he confirms it ran ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2.8).
4. With `browse`, open each of the ticket's forms in every view in the configuration, and save a screenshot of each.
5. Compare each form with its approved screen requirement, element by element. Check theme usage against the inventory and `DESIGN.md`, accessibility against `spec-ui-standards` section 13, the always-available controls, and page addresses and browser storage for anything sensitive.
6. Write each finding with its form, evidence and severity; with none, write the clean-pass statement. Change no form.
7. Record every test in the checks file, naming its evidence.
8. Run the Full BFT. Complete the Step 36 `steps` row with the ledger values in the configuration, and write the BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
9. Explain what was done. Present the Step Receipt and stop.
