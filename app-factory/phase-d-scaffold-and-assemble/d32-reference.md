---
title: "d32-reference"
doc-id: "mb-709975a7"
updated: "2026-11-12"
---
# Step 32 — Create the Scaffold: Reference

What the agent does at Step 32, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d32-config|Step 32 Configuration]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d32-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2).

## 1. Start

1. Read the entry record and Step 31's ledger row. Check Step 31 is complete for this run (test PR-01). If not: stop and raise a deviation.
2. Read every input in the configuration.

## 2. The stubs

3. For each module and function `scaffold-spec.md` plans that does not exist in the app: create it with `server-code` or `client-modules`, in the stub form in the configuration. Leave every existing module marked keep or rework as it is, and remove nothing.
4. Create nothing the plan does not name, and no form.
5. Fill the app's `tests\ts-config.yaml` with the scanner settings. Keep its theme keys as they are.
6. Write the stub list.

## 3. Checks

7. Run `anvil --json validate .` (test ST-01) and `ts_scan.py` (test ST-10). On a failure in a file this step created: correct it and run again. On a failure in an existing file: record it for Step 34.
8. Check that every planned function exists and that nothing unplanned was created. Record the results in the checks file.

## 4. The push

9. Give David the command in the configuration and wait until he confirms it ran (test PR-06).

## 5. The end

10. Run the Light BFT. Complete the Step 32 `steps` row with the ledger values in the configuration, and write the BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
11. Explain what was done. Present the Step Receipt, stop, and ask David to run `/mb-close-out`.
