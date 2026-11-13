---
title: "e40-reference"
doc-id: "mb-e275399d"
updated: "2026-11-13"
---
# Step 40 — Architecture Scan: Reference

What the agent does at Step 40, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-e-build-and-verify/e40-config|Step 40 Configuration]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2).

1. Read the entry record and the ledger row of Step 35A for this ticket. Check it is complete or skipped (test PR-01). If not: stop and raise a deviation.
2. Read the ticket, and every input in the configuration.
3. Ask David whether the scan runs for this ticket. On no: record the step `skipped`, write the receipt, stop.
4. Refresh the code graph with `graphify`. Run `improve-codebase-architecture` read-only. Write each finding to the scan report.
5. Present each finding to David with your recommendation; record his decision.
6. Run the Light BFT. Complete the Step 40 `steps` row with the ledger values in the configuration, and write the BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
7. Explain what was done. Present the Step Receipt and stop.
