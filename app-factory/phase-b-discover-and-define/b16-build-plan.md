---
title: "b16-build-plan"
doc-id: "mb-625b446e"
updated: "2026-10-24"
---
# Step 16 — Domain Modeling: Build Plan

## Step entry

### Phase B — Discover and Define

Ends with the gate `domain-locked` (this step).

#### Step 16: Domain modeling

**Must achieve:** the business's vocabulary fixed, so that a term means the same thing in every later step and every app; the decisions that are hard to reverse recorded; the glossary and the data design in agreement; and Phase B closed: every Phase B output complete, tested and approved, and locked by David at the gate `domain-locked`, so that Phase C builds on a settled foundation.

**Starts from:** the items Step 15 handed over (the reviewed plan, the test plan, the app's access matrix and threat model, and Step 15's receipt); the business's `docs-local\GLOSSARY.md` and `adr-local\`, when they exist; for an existing application, its existing glossary under any name, its decision records and its code graph, as prior material; the ledger rows and receipts of every Phase B step of this run; `spec-nomenclature`.

**Produces:** `docs-local\GLOSSARY.md`, the business's glossary, shared by all its apps; any ADR in `adr-local\` (`adr-{kebab-case-name}.md`); the plan's Architecture section brought into agreement with the glossary; the domain map in `pdlf-outputs\b16\`; the Phase B close-out check; the `gates` row of `domain-locked`; in `pdlf-outputs\b16\`: the copies, the test results and the Step Receipt; the ledger row, the BFT record and Sentinel's `triage_findings` row.

**Carried out by:** OpenCode, with Matt Pocock's `grill-with-docs` (which runs `grilling` with `domain-modeling`), Anvil's `data-models`, `graphify`, Matt Pocock's `prototype` when an entity's life is uncertain, `mb-archify-scope` with `archify`, and `mb-sentinel-review`. David answers the interview, decides each ADR and passes or blocks the gate.

**Must be built so that:**
- `grill-with-docs` is started from the project library and runs as the skill is designed: `grilling` maps the design tree and asks each round's whole frontier, each question with its recommended answer, and waits for David; `domain-modeling` challenges terms against the glossary, sharpens fuzzy language, tests relationships with concrete scenarios and writes each settled term into the glossary at once; PDLF never limits or reshapes the questions;
- the skill is given the full text of every item from Step 15, the glossary and decisions that exist, and the context pack, with these destinations and answers fixed in the invocation: the glossary is `docs-local\GLOSSARY.md`, in the skill's own `GLOSSARY-FORMAT.md`, single context; decisions go to `adr-local\` as `adr-{kebab-case-name}.md`, in the skill's own `ADR-FORMAT.md`, not to `docs/adr/` with numbers; facts are looked up by the agent in the main session, because Cupcake blocks sub-agents, and David is asked only for decisions;
- the glossary holds the terms of this business only, with no implementation detail; a term the business shares with another Mybizz application or a system keeps the name `spec-nomenclature` gives it; the term "multi-tenant" is never used for the five-app model; where the application follows a reference platform, each of the reference's domain terms is adopted or renamed in the glossary;
- an ADR is offered only for a decision that is hard to reverse, surprising without context and the result of a real trade-off, and written only with David's approval;
- every open question the plan gives to Step 16 is settled and removed from Open Questions, so that Open Questions is empty when Phase B closes;
- for an existing application, `domain-modeling` checks what the documents say against the code through the code graph and shows David every contradiction; an existing glossary under another name (such as `CONTEXT.md`) and its decisions are prior material: their terms are reconciled with the data design before any term is settled, the settled terms are written into `GLOSSARY.md`, and David decides whether the old file is removed;
- for a feature, the glossary and the decisions are extended, never rewritten; for App 5, its terms join the same glossary, because the business has one vocabulary;
- Anvil's `data-models` is used to check that the glossary and the data design agree: every entity in the glossary has an owner and a place in the data design, and the data design uses only the glossary's terms; each mismatch is corrected with David in the glossary or in the plan's Architecture section, and GStack's report stays the last section of the plan;
- an entity whose life is uncertain is proven with `prototype` (logic branch) before its terms are settled;
- the domain map (the entities and their relationships) is scoped with `mb-archify-scope` and drawn with `archify` into the step folder, and the glossary is not changed by it;
- the security review `mb-sentinel-review` runs on the glossary and the ADRs at Low/Medium scrutiny, against the documents Sentinel names for Step 16 (the threat models matching the entities, and `sec-requirements-data-table-creation`, because Step 17 builds the tables from this vocabulary); a Flag or Escalate stops the step and goes to David; its `triage_findings` row is checked before the gate;
- before the gate, the agent closes Phase B with one check of the whole run: every Phase B step of the run (Steps 11, 12, 14, 15 and 16 for a whole application; Steps 12, 14, 15 and 16 for a feature) has its ledger row complete and its Step Receipt; every receipt matches its evidence (test PR-05, `ts_report.py --check`); every test of every Phase B test specification passed; every Sentinel finding of the run has David's decision; the plan's Open Questions section is empty; every hand-over item Phase C reads exists; every input notice is carried;
- the gate follows `spec-gate-procedure`: Full BFT, the gate summary block, which lists Phase B's outputs and the result of the close-out check, and David's explicit yes or no; on yes the `gates` row is written with its approval time; on no the step stops and records the blocker; the gate is never passed by the agent;
- after the gate, no term is added and no Phase B output is changed without the gate being reopened by a deviation David authorises;
- it hands to Phase C (Step 17 first) the glossary, the ADRs, the reviewed plan with its data design, the test plan, the access matrix, the threat model, the domain map and its Step Receipt;
- its ledger row is `step_type = 'gate'`, `skill_family = 'matt-skills'`, `synthesized = false`, `run` and `app_number` from the entry record, and `inputs_used` naming Step 15.

**BFT level:** Full (gate).

**Gate:** `domain-locked`: the glossary, its decisions and the data design they agree with, and with them every output of Phase B, are locked; Phase C builds on them.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md), [[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), [[[pdlf:pdlf-library/specifications-local/spec-skill-context-pack|Spec: Skill Context Pack]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-context-pack.md), [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `grill-with-docs`, running `grilling` with `domain-modeling` (Matt Pocock) → the glossary and the ADRs, then every later step.
- `data-models` (Anvil): the glossary and the data design checked against each other → Step 17's tables.
- `graphify`: for an existing application, the documents checked against the code → the contradictions shown to David.
- `prototype` (Matt Pocock), logic branch, only for an entity whose life is uncertain → the glossary and the ADRs.
- `mb-archify-scope`, then `archify`: the domain map → David at the gate, then Step 17.
- `mb-sentinel-review`, Low/Medium → `triage_findings`.

**Layers with no skill:** display (screens are designed at Steps 22 to 26).

**Testing:** [[[pdlf:app-factory/phase-b-discover-and-define/b16-test-spec|Step 16 Test Specification]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-test-spec.md): the vocabulary is sound, Phase B's tests all passed and its receipts match their evidence, and the gate has David's approval.

**Standards:** [[[default:specifications-global/spec-nomenclature|Spec: Nomenclature]]](C:/dev/project-library-global/specifications-global/spec-nomenclature.md): terms common to every application, every system and PDLF; the glossary holds only this business's terms.

## Why it is built this way

- **The skill's own pair.** `grill-with-docs` is Matt Pocock's composition of the interview and the domain discipline; running it as designed gets both, and its files use the skill's own names so every later Matt Pocock skill reads them.
- **One glossary for the business.** All the business's apps serve one domain; one glossary keeps a term identical in App 1, App 5 and every feature.
- **The glossary and the data design agree.** Step 17 builds the tables from the data design; a table named differently from the glossary would split the vocabulary from its first build.
- **Phase B is closed in one check.** The gate locks everything Phase B produced, so it is offered only when every step of the phase is complete, tested and approved, and every question is answered.
- **David passes the gate.** The gate is the hard stop before tables are built in Anvil; only David's yes lets Phase C begin.
