---
title: "b16-reference"
doc-id: "mb-741c244a"
updated: "2026-10-29"
---
# Step 16 — Domain Modeling: Reference

What the agent does at Step 16, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-b-discover-and-define/b16-config|Step 16 Configuration]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md), and the gate ceremony in [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md); neither is repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2).

## 1. Start

1. Read the entry record and Step 15's ledger row. Check Step 15 is complete for this run and its outputs approved (test PR-01). If not: stop and raise a deviation.
2. Carry forward every input notice of Steps 12 to 15 to this step's receipt.
3. Read every input in the configuration, including the glossary and decisions that exist.
4. For an existing application: find any existing glossary, under any name, and its decision records, and query the code graph of the app folder. Treat all of it as prior material.

## 2. The interview

5. Start `grill-with-docs` from the project library, `C:\dev\dev-{slug}\{slug}-project-library`. Paste the full text of every input and the context pack. State the fixed answers and the vocabulary rules in the configuration.
6. `grilling` asks each round's frontier, each question with its recommended answer; David answers. Look up every fact yourself. Never limit or reshape the questions.
7. As each term is settled, `domain-modeling` writes it into `docs-local\GLOSSARY.md` at once, in its `GLOSSARY-FORMAT.md`. For a feature or App 5, extend the glossary; never rewrite it.
8. Apply the vocabulary rules: shared names from `spec-nomenclature`; never "multi-tenant" for the five-app model; a reference platform's terms adopted or renamed.
9. For an existing application: `domain-modeling` checks each statement against the code graph and shows David each contradiction. Reconcile the prior glossary's terms with the data design before settling them, and write them into `GLOSSARY.md`. Ask David whether the old glossary file is removed.
10. When a decision is hard to reverse, surprising without context and the result of a real trade-off, offer an ADR. On David's yes, write `adr-local\adr-{kebab-case-name}.md` in the skill's `ADR-FORMAT.md`.
11. For an entity whose life is uncertain: build a `prototype`, logic branch, as `pdlf-outputs\b16\{slug}-b16-{run}-prototype-{entity}.html`. David drives it. Settle its terms from the verdict.
12. Settle every open question the plan gives to Step 16 and remove it from Open Questions.
13. Continue until the frontier is empty and David confirms the shared understanding.

## 3. Glossary and data design

14. Apply `data-models` to check the glossary against the plan's data design: every entity in the glossary has an owner and a place in the data design, and the data design uses only the glossary's terms.
15. Correct each mismatch with David, in the glossary or in the Architecture section of `design-doc.md`. Keep GStack's report the last section of the plan.

## 4. The domain map

16. Run `mb-archify-scope` for the domain map (the entities and their relationships); David approves the Scope Card. Run `archify` into `pdlf-outputs\b16\`.

## 5. Checks

17. Check the glossary against test DC-09. Record the result in `pdlf-outputs\b16\{slug}-b16-{run}-checks.xml`, naming the terms that show it. On a failure: correct with David and check again.
18. Run `mb-sentinel-review` for Step 16 at Low/Medium scrutiny on the glossary and the ADRs. On Flag or Escalate: stop and present it to David. Check the review's `triage_findings` row exists.
19. Run `gitleaks` on the project library's working tree (test PR-06) and save its report as `pdlf-outputs\b16\{slug}-b16-{run}-gitleaks.json`. A secret found: remove it, then run again. Record PR-06 in the checks file.
20. Copy `GLOSSARY.md` and each ADR written into `pdlf-outputs\b16\` under the names in the configuration.

## 6. Closing Phase B

21. Run every check of the Phase B close-out check in the configuration. Run `ts_report.py` with `--check` on each Phase B receipt of the run (test PR-05). Write the results to `pdlf-outputs\b16\{slug}-b16-{run}-phase-b-close.md` and record PR-05 and PR-04 in the checks file.
22. If any check fails: present it to David, correct it at its source, and run the check again. Never offer the gate while a check fails.

## 7. The gate

23. Run the Full BFT for the gate.
24. Present the gate summary block in the configuration, with the outputs it locks and the close-out result. Ask David: "Proceed to Phase C? (yes/no)".
25. On no: record the blocker, set the step's `status` to `blocked`, stop.
26. On yes: give David the command that records his approval, `bash /mnt/c/mybizz/scripts/pdlf-gate.sh {slug} domain-locked {run}`, and wait until he confirms it ran. Never run it and never write to the `gates` table. Read the `gates` row and check `domain-locked` is passed for the run; if it is not, stop. Record PR-03 in the checks file.

## 8. The end

27. Complete the Step 16 `steps` row with the ledger values in the configuration, and write the Step Receipt and the Full BFT record.
28. Explain what was done and why, and that Phase B is closed and Phase C begins at Step 17. Present the Step Receipt, stop, and ask David to run `/mb-close-out`.
