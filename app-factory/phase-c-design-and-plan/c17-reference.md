---
title: "c17-reference"
doc-id: "mb-0ecf17ed"
updated: "2026-11-12"
---
# Step 17 — Create Anvil Data Tables: Reference

What the agent does at Step 17, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-c-design-and-plan/c17-config|Step 17 Configuration]]](C:/pdlf/app-factory/phase-c-design-and-plan/c17-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2). How a schema change reaches the tables: [[[default:anvil-docs/ai-agent/anvil-ai-agent|The Anvil AI Agent]]](C:/dev/project-library-global/anvil-docs/ai-agent/anvil-ai-agent.md).

## 1. Start

1. Read the entry record and Step 16's ledger row. Check Step 16 is complete for this run and the gate `domain-locked` is passed (test PR-01). If not: stop and raise a deviation.
2. Carry forward every input notice of Step 16 to this step's receipt.
3. Read every input in the configuration.

## 2. The authoritative schema

4. If `authoritative-schema.md` holds no tables: write it from the data design with `data-models`, in the structure the project template gives the file, applying the schema rules in the configuration. Present it to David and wait for his approval. Never continue without it.
5. If it holds tables: check it against the data design, table by table. On any disagreement: stop and raise a deviation.
6. Run `secure-software-engineering` on the schema against Step 15's threat model and trust boundaries. Correct each finding with David, in the authoritative schema.

## 3. The difference list

7. Compare the authoritative schema with `db_schema` in App 1's `anvil.yaml`. Write every difference to the schema difference list, sorted by kind as the configuration sets out: additions, renames, removals, type changes.
8. Take each rename from `schema-migration-log.md`. Where a column disappears and another appears in the same table with no log row, ask David whether it is a rename.
9. For a feature run: any rename, removal or type change is a breaking change. Name each one to David and apply it only with his approval.

## 4. Renames, by hand

10. If the list has renames: write David's numbered rename instructions with `wizard`, one rename per instruction, each naming the table, the old name and the new name, in the Data Tables view. Wait until David confirms every rename is done.
11. Give David the pull command in the configuration and wait until he confirms it ran. Check that `anvil.yaml` now shows every rename. If not: stop and raise a deviation.

## 5. The schema in `anvil.yaml`

12. Write the whole authoritative schema into `db_schema` in `anvil.yaml`, only through the `anvil-yaml` skill. Never change `dependencies`.
13. Run `anvil --json validate anvil.yaml` (test ST-01). On an error: correct it and run again.
14. Compare `db_schema` with the authoritative schema, table by table and column by column. On any difference: correct `anvil.yaml` and compare again.
15. Run `ts_scan.py` on App 1 and save its report (tests ST-06 and ST-07). On a failure: correct the authoritative schema with David, then repeat from step 12.

## 6. Applying the schema

16. Write David's numbered instructions with `wizard`: the commit command in the configuration; open App 1 in the Anvil editor; click Resolve in the Data Tables view; apply each addition; check each removal and type change by name against the difference list before applying it. List every removal and type change by name in the instructions.
17. Wait until David confirms the Data Tables view no longer reports a schema mismatch. If he reports a difference the list does not hold: stop and raise a deviation.
18. Add one row per change to `schema-migration-log.md`, with its migration plan.

## 7. Checks

19. Run `mb-sentinel-review` for Step 17 at High scrutiny on the authoritative schema and `db_schema`. On Flag or Escalate: stop and present it to David. Check the review's `triage_findings` row exists (test PR-04).
20. Copy the authoritative schema and the `db_schema` section into `pdlf-outputs\c17\` under the names in the configuration. Record every test result in the checks file, naming its evidence.

## 8. The end

21. Run the Light BFT. Complete the Step 17 `steps` row with the ledger values in the configuration, and write the BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
22. Explain what was done and why. Present the Step Receipt, stop, and ask David to run `/mb-close-out`.
