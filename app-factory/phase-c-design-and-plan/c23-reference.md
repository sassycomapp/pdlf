---
title: "c23-reference"
doc-id: "mb-9de2903a"
updated: "2026-11-12"
---
# Step 23 — Design Review: Reference

What the agent does at Step 23, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-c-design-and-plan/c23-config|Step 23 Configuration]]](C:/pdlf/app-factory/phase-c-design-and-plan/c23-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2).

## 1. Start

1. Read the entry record and Step 22's ledger row. Check Step 22 is complete for this run (test PR-01). If not: stop and raise a deviation.
2. Hand David `mg-grant --path ~/.gstack --count 15` and wait until he confirms it ran ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2.8). Carry forward every input notice of Step 22 to this step's receipt.
3. Read every input in the configuration, including the theme's whole component documentation.

## 2. The reviews

4. Run `/plan-design-review` on the screen requirements and `DESIGN.md`, with the fixed answers in the configuration. Write its ratings and each gap it finds into the design review as findings.
5. For each screen requirement, compare every element with the whole inventory. For each element a better-fitting theme component would serve, write a high finding naming that component and why it fits better.
6. Check every screen requirement against `spec-ui-standards` sections 12 and 13, and write each gap as a finding.
7. Give every finding its requirement, element, proposed correction and severity, by the severity table in the configuration. Ask David to rate any finding the table does not settle.
8. Change no screen requirement.

## 3. Checks

9. Check that every screen requirement in the index has its review entry, and record the result in the checks file (test DC-16, theme usage).

## 4. The end

10. Run the Full BFT. Complete the Step 23 `steps` row with the ledger values in the configuration, and write the BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md), with the number of findings by severity.
11. Explain what was done. Present the Step Receipt, stop, and ask David to run `/mb-close-out`.
