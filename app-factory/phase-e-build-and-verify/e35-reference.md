---
title: "e35-reference"
doc-id: "mb-a32fbe97"
updated: "2026-11-13"
---
# Step 35 — Build: Reference

What the agent does at Step 35, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-e-build-and-verify/e35-config|Step 35 Configuration]]](C:/pdlf/app-factory/phase-e-build-and-verify/e35-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2). The per-feature method is [[[default:specifications-global/mo-ui-production|UI Production Method]]](C:/dev/project-library-global/specifications-global/mo-ui-production.md) section 4; its order is in the configuration.

## 1. Start

1. Read the entry record and the ledger row of Step 34 for this ticket. Check it is complete or skipped (test PR-01). If not: stop and raise a deviation.
2. Read the ticket, and every input in the configuration.
3. Check that the ticket, its approved screen requirements, the authoritative schema and the SRS agree. On a disagreement: stop and present it to David; a change to an approved screen requirement needs his approval.
4. Give David the command that starts the local runtime, and wait until he confirms it ran.

## 2. Server code

5. For each behaviour the ticket names, write its test first with `tdd`, then fill its stub with `server-code`, `client-modules` and `data-models`, inside the module `scaffold-spec.md` sets. Build and test the ticket's security criteria with `secure-software-engineering`. Change any app setting only through `anvil-yaml`. If the feature needs a table that does not exist: stop and raise a deviation to Step 17.
6. Run Level 0 (`anvil --json validate`, `ts_scan.py`), Level 1 and Level 2. On a failure: find its root cause with `diagnosing-bugs`, fix it, run the level again.
7. Add each new server function to `access-matrix.yaml`. Write the review package (the changed server code, the ticket, the screen requirements) for Claude, and give it to David. Correct each finding Claude returns, then run step 6 again.
8. Give David the commit commands in the configuration, written with `wizard`, and wait until he confirms they ran.

## 3. Forms

9. Run `mb-form-builder` for the ticket's forms. It removes the old forms the ticket replaces.
10. Write the review package (each form, its spec sheet, its screen requirement) for Claude, and give it to David. Correct each finding.
11. Give David the commit commands, then his instructions, written with `wizard`, to open each form in Anvil. Success: every component shows, nothing is reported missing, and the form looks as its screen requirement describes.
12. Give David the wiring task for Anvil's agent, word for word as `mo-ui-production` section 4 sets it, with the ticket's forms by module path, then `/review-commit`. Wait until he confirms both ran.
13. Give David the pull command; then run `anvil --json validate client_code` and `ts_scan.py`. Write the review package of the Anvil agent's commit for Claude. On any change beyond handler bodies: give David the correction for Anvil's agent, and repeat from step 12.

## 4. Rework and Level 3

14. Clear the ticket's items on the rework list, and remove the modules the disposition list marks remove for this ticket. Run Levels 0 to 2 again.
15. Give David his Level 3 instructions, written with `wizard`: every flow of the ticket in the browser on hosted App {n}, at desktop and phone width, with `TEST_` data only. Remove the `TEST_` data afterwards.
16. Ask David to sign the feature off against its ticket and its screen requirements (test BR-09).

## 5. Checks

17. Record every test in the checks file, naming its evidence.
18. Run `mb-sentinel-review` for Step 35 at High scrutiny on the feature's code. On Flag or Escalate: stop and present it to David. Check the review's `triage_findings` row exists (test PR-04).

## 6. The end

19. Run the Full BFT. Complete the Step 35 `steps` row with the ledger values in the configuration, and write the BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
20. Explain what was done. Present the Step Receipt and stop.
