---
title: "d33-reference"
doc-id: "mb-768f1d0a"
updated: "2026-11-12"
---
# Step 33 — Pull to Local: Reference

What the agent does at Step 33, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d33-config|Step 33 Configuration]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d33-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2).

1. Read the entry record and Step 32's ledger row. Check Step 32 is complete for this run (test PR-01). If not: stop and raise a deviation.
2. Run Step 18's procedure, sections 2 to 4 of [[[pdlf:app-factory/phase-c-design-and-plan/c18-reference|Step 18 Reference]]](C:/pdlf/app-factory/phase-c-design-and-plan/c18-reference.md), with the expected change in this step's configuration, and with Step 33's outputs and ledger values.
3. Explain what was done. Present the Step Receipt, stop, and ask David to run `/mb-close-out`.
