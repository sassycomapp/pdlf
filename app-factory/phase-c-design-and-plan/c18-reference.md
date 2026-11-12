---
title: "c18-reference"
doc-id: "mb-f52c6985"
updated: "2026-11-12"
---
# Step 18 — Pull to Local: Reference

What the agent does at Step 18, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-c-design-and-plan/c18-config|Step 18 Configuration]]](C:/pdlf/app-factory/phase-c-design-and-plan/c18-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2).

## 1. Start

1. Read the entry record and Step 17's ledger row. Check Step 17 is complete for this run (test PR-01). If not: stop and raise a deviation.

## 2. The pull

2. Give David the command in the configuration and wait until he confirms it ran.

## 3. Checks

3. Run every check in the configuration, in order. Record each result in the checks file.
4. On a failed check: stop, present it to David and raise a deviation. Never correct the app in this step.

## 4. The end

5. Complete the Step 18 `steps` row with the ledger values in the configuration, and write the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md), recording the commit `master` now points to.
6. Explain what was done. Present the Step Receipt, stop, and ask David to run `/mb-close-out`.
