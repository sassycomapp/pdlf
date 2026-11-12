---
title: "c19-reference"
doc-id: "mb-72bd1c28"
updated: "2026-11-12"
---
# Step 19 — Tickets: Reference

What the agent does at Step 19, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-c-design-and-plan/c19-config|Step 19 Configuration]]](C:/pdlf/app-factory/phase-c-design-and-plan/c19-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2).

## 1. Start

1. Read the entry record and Step 18's ledger row. Check Step 18 is complete for this run (test PR-01). If not: stop and raise a deviation.
2. Carry forward every input notice of Steps 16 to 18 to this step's receipt.
3. Read every input in the configuration.

## 2. The tickets

4. Start `to-tickets` with the reviewed plan, the test plan, the glossary and the ADRs. Give it the ticket format, the ticket contents and the build order in the configuration.
5. Write the tickets to `pdlf-tickets\{run}\`. For a feature run, write only the feature's tickets and record the release's version on each.
6. Name every form by module path, with its package from `ui\README.md`. Name every table as the authoritative schema names it.
7. Run `secure-software-engineering` on each ticket against Step 15's threat model, and write its security criteria into the ticket.
8. Check: every feature of the plan has a ticket; every ticket belongs to a feature; the order has no cycle; every shared custom component comes before the tickets that use it. Correct each failure.
9. Write the ticket list, in build order, with each ticket's forms.

## 3. The flows

10. Run `mb-archify-scope` for the user flows and for each ticket that spans more than one form; David approves each Scope Card. Run `archify` into `pdlf-outputs\c19\`.

## 4. Approval

11. Present the ticket list to David. Correct each change he asks for in the tickets, and present it again until he approves it.

## 5. Checks

12. Check the tickets against test DC-10 and record the result in the checks file, naming the tickets that show it.
13. Run `mb-sentinel-review` for Step 19 at Medium scrutiny on the tickets. On Flag or Escalate: stop and present it to David. Check the review's `triage_findings` row exists (test PR-04).

## 6. The end

14. Run the Full BFT. Complete the Step 19 `steps` row with the ledger values in the configuration, and write the BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
15. Explain what was done. Present the Step Receipt, stop, and ask David to run `/mb-close-out`.
