---
title: "d31-reference"
doc-id: "mb-3689e5a4"
updated: "2026-11-12"
---
# Step 31 — Scaffold Plan: Reference

What the agent does at Step 31, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d31-config|Step 31 Configuration]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d31-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2).

## 1. Start

1. Read the entry record and Step 26's ledger row. Check Step 26 is complete and `screens-approved` is passed for this run (test PR-01). If not: stop and raise a deviation.
2. Carry forward every input notice of Steps 17 to 26 to this step's receipt.
3. Read every input in the configuration.

## 2. Existing app

4. For an existing app: build the code graph of `client_code` and `server_code` with `graphify`. Keep it for step 9.

## 3. The structure

5. Run `codebase-design` on the reviewed plan's architecture to shape the modules: deep modules at clean seams, business logic in pure modules apart from Anvil code.
6. Apply `data-models` to decide where each table's behaviour lives. Apply `server-code` and `client-modules` to place and name every module.
7. Plan every function, with the fields in the configuration. Every server function a screen requirement names gets its planned function, with the same name. Plan the common aspects' modules in the one structure `adr-common-architecture-across-mybizz-applications` sets. Plan every shared custom component as its own module.
8. Write `scaffold-spec.md`, section by section, as the configuration sets out. For a feature run, extend it; never rewrite it.
9. For an existing app: list every existing module and server function as keep, rework or remove, each rework and remove naming its ticket. Write the disposition list. Change no code.
10. Write the scanner settings from the structure.

## 4. Approval

11. Present `scaffold-spec.md` and, for an existing app, the disposition list to David. Correct each change he asks for, and present them again until he approves them.

## 5. Checks

12. Check every screen requirement's server functions and every ticket against the planned functions, and every planned function for its access rule and test ID. Record the results in the checks file (test DC-10). On a failure: correct `scaffold-spec.md` and check again.
13. Copy `scaffold-spec.md` into the step folder.

## 6. The end

14. Run the Full BFT. Complete the Step 31 `steps` row with the ledger values in the configuration, and write the BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
15. Explain what was done. Present the Step Receipt, stop, and ask David to run `/mb-close-out`.
