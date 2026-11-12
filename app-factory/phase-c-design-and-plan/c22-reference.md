---
title: "c22-reference"
doc-id: "mb-56ecf085"
updated: "2026-11-12"
---
# Step 22 — Screen Requirements: Reference

What the agent does at Step 22, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-c-design-and-plan/c22-config|Step 22 Configuration]]](C:/pdlf/app-factory/phase-c-design-and-plan/c22-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2).

## 1. Start

1. Read the entry record and Step 21's ledger row. Check Step 21 is complete and `concept-locked` is passed for this run (test PR-01). If not: stop and raise a deviation.
2. Carry forward every input notice of Steps 19 to 21 to this step's receipt.
3. Read every input in the configuration. Read the theme's `base-inventory.md` and every file in `docs\components\` in full before writing any screen requirement.

## 2. The screen requirements

4. List every form the tickets name, by module path, in the tickets' build order. For an existing application, also list every existing form in `client_code` that no ticket names. Write the requirement index.
5. For each ticket, write the screen requirement of each of its forms from the model, at `ui\<package path>\<FormName>\<FormName>-requirement.md`, with `status: draft`:
   1. Section 1: module path, purpose, screen type and width from `spec-ui-standards` section 7, layout form, route.
   2. Section 2: every element, with the component chosen by the component choice rule in the configuration, the reason it serves better than the other candidates, its role, its `wrap_on` and its tooltip phrase key. Use only properties, events and values the theme's documentation gives.
   3. Section 3: the table and column of the authoritative schema each element shows.
   4. Section 4: every action, with its event handler `<component name>_<event>`, the server function its ticket names and the result.
   5. Section 5: the empty state's four parts.
   6. Section 6: the scope of every role of the access matrix.
   7. Section 7: every phrase key with its English text, in the tone `DESIGN.md` sets.
   8. Section 8: every process on the form and its help video.
   9. Section 9: every user flow the form takes part in.
6. Where the documents do not settle a point, ask David, with your recommended answer. Never guess a component, property, column or function.
7. Add every form missing from `access-matrix.yaml` under `forms`, keyed by module path, with the scopes of section 6.

## 3. Checks

8. Check every screen requirement against test DC-16 and every form against DC-05's form rows. Record the results in the checks file, naming the requirements that show them. On a failure: correct the requirement and check again.

## 4. The end

9. Run the Full BFT. Complete the Step 22 `steps` row with the ledger values in the configuration, and write the BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md), listing every existing form no ticket names.
10. Explain what was done. Present the Step Receipt, stop, and ask David to run `/mb-close-out`.
