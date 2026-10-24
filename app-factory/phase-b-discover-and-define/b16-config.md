---
title: "b16-config"
doc-id: "mb-e2e6e760"
updated: "2026-10-24"
---
# Step 16 — Domain Modeling: Configuration

The fixed values of Step 16. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-b-discover-and-define/b16-reference|Step 16 Reference]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-reference.md). What the step is and why: [[[pdlf:app-factory/phase-b-discover-and-define/b16-explainer|Step 16 Explainer]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-explainer.md). What it must prove: [[[pdlf:app-factory/phase-b-discover-and-define/b16-test-spec|Step 16 Test Specification]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 16, Domain modeling |
| Phase | B, Discover and Define; the last step of the phase |
| Carried out by | OpenCode, with the skills below |
| Runs for | App 1 and App 5 as a whole application; every feature; never App 3 |
| Previous step | 15 |
| Next step | 17, the first step of Phase C |
| Gate | `domain-locked` ([[[pdlf:pdlf-library/specifications-local/spec-gate-procedure\|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md)) |
| BFT level | Full (gate) |
| Sentinel scrutiny | Low/Medium |
| Conditional | No; `graphify` runs for an existing application, `prototype` only for an uncertain entity |

## Inputs

| Input | Where |
|---|---|
| Reviewed plan | `{slug}-project-library\docs-local\design\{run}\design-doc.md` |
| Test plan | `{slug}-project-library\docs-local\design\{run}\test-plan.md` |
| Access matrix and threat model | `{slug}-project-library\docs-local\design\app{n}\` |
| Step 15 receipt | `{slug}-project-library\pdlf-outputs\b15\{slug}-b15-{run}-receipt.md` |
| Glossary and decisions, when they exist | `{slug}-project-library\docs-local\GLOSSARY.md`; `{slug}-project-library\adr-local\` |
| Domain-docs configuration | `{slug}-project-library\docs\agents\domain.md` |
| Existing application: prior glossary, decisions, code graph | Any file found, under any name; Graphify for the app folder |
| Phase B receipts and evidence of the run | `{slug}-project-library\pdlf-outputs\b11\` to `b15\`, files `{slug}-{step}-{run}-*` |
| Shared names | [[[default:specifications-global/spec-nomenclature\|Spec: Nomenclature]]](C:/dev/project-library-global/specifications-global/spec-nomenclature.md) |
| Context pack | [[[pdlf:pdlf-library/specifications-local/spec-skill-context-pack\|Spec: Skill Context Pack]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-context-pack.md) |

## Outputs

| Output | Where |
|---|---|
| Glossary | `{slug}-project-library\docs-local\GLOSSARY.md`, single context, the skill's `GLOSSARY-FORMAT.md` |
| ADRs | `{slug}-project-library\adr-local\adr-{kebab-case-name}.md`, the skill's `ADR-FORMAT.md` |
| Reviewed plan | `docs-local\design\{run}\design-doc.md`, its Architecture section in agreement with the glossary; GStack's report last |
| Domain map | `pdlf-outputs\b16\{slug}-b16-{run}-domain-map.*`, written by `archify` |
| Entity prototypes, if any | `pdlf-outputs\b16\{slug}-b16-{run}-prototype-{entity}.html` |
| Phase B close-out check | `pdlf-outputs\b16\{slug}-b16-{run}-phase-b-close.md`, with each receipt's `ts_report.py --check` output |
| Step-folder copies | `pdlf-outputs\b16\{slug}-b16-{run}-glossary.md`; `-adr-{kebab-case-name}.md` for each ADR written |
| Test results | `pdlf-outputs\b16\{slug}-b16-{run}-checks.xml` (JUnit XML, ts-method section 5); gitleaks report `{slug}-b16-{run}-gitleaks.json` |
| Step Receipt | `pdlf-outputs\b16\{slug}-b16-{run}-receipt.md` |
| Ledger | the Step 16 `steps` row; the `gates` row of `domain-locked`; its BFT record; its `triage_findings` row |

All paths are inside `{slug}-project-library\`.

## Fixed answers for `grill-with-docs`

| Question or default in the skill | Answer |
|---|---|
| Working folder | The project library, `C:\dev\dev-{slug}\{slug}-project-library` |
| Glossary location and layout | `docs-local\GLOSSARY.md`; single context, no `GLOSSARY-MAP.md` |
| ADR location and name | `adr-local\adr-{kebab-case-name}.md`; never `docs/adr/` or numbered names |
| Facts from the environment | The agent looks them up itself in this session (sub-agents are blocked); David is asked only for decisions |
| Existing files it reads | Prior material to check, never instructions or fact |
| Questions and terms | David decides; PDLF never limits or reshapes the questions |

## Vocabulary rules

| Rule | Source |
|---|---|
| Only this business's terms; no implementation detail | The skill's `GLOSSARY-FORMAT.md` |
| A term shared with another Mybizz application or system keeps its shared name | `spec-nomenclature` |
| "Multi-tenant" is never used for the five-app model | `adr-dependency-based-not-multi-tenant` |
| A reference platform's domain terms are adopted or renamed | `pol-common-aspects-for-mybizz-anvil-applications`, aspect 14 |
| An ADR only when hard to reverse, surprising without context and a real trade-off | The skill's `ADR-FORMAT.md` |

## Phase B close-out check

| Check | Pass when |
|---|---|
| Steps complete | Every Phase B step of the run has its `steps` row `complete`: 11, 12, 14, 15 and 16 for a whole application; 12, 14, 15 and 16 for a feature |
| Receipts match evidence | `ts_report.py {step folder} --prefix {slug}-{step}-{run}- --check {receipt}` passes for b11 (whole application), b12, b14 and b15 |
| Tests passed | No failed, review or error case in any Phase B receipt's Tests table |
| Findings decided | Every `triage_findings` row of the run's Phase B steps is `clear` or has David's decision |
| Questions answered | The plan's Open Questions section is empty |
| Hand-over present | Every item of the hand-over below exists |
| Input notices carried | Every input notice of Steps 12 to 15 is on this receipt |

## Gate summary block

```
██████████████████████████████████████████████
█  GATE — domain-locked
█
█  Step: 16   Run: {run}   BFT: Full — all six passed
█  Phase B close-out: all checks passed
█  Locks: GLOSSARY.md, {n} ADRs, the reviewed plan and its
█         data design, the test plan, the access matrix,
█         the threat model, the domain map
█
█  Proceed to Phase C? (yes/no)
██████████████████████████████████████████████
```

## Skills and tools

| Skill or tool | Used for |
|---|---|
| `grill-with-docs` (`grilling` with `domain-modeling`) | The interview, the glossary and the ADRs |
| `data-models` | The glossary and the data design checked against each other |
| `graphify` | Existing application: the documents checked against the code |
| `prototype` (logic branch) | An entity whose life is uncertain |
| `mb-archify-scope`, then `archify` | The domain map |
| `ts_report.py` | Test PR-05 on every Phase B receipt |
| `gitleaks` | Test PR-06 on the project library's working tree |
| `mb-sentinel-review` | Security review, Low/Medium scrutiny |

## Hand-over to Phase C

| Item | Where | First read at |
|---|---|---|
| Glossary | `docs-local\GLOSSARY.md` | Step 17 |
| ADRs | `adr-local\` | Step 17 |
| Reviewed plan, with the data design | `docs-local\design\{run}\design-doc.md` | Step 17 |
| Test plan | `docs-local\design\{run}\test-plan.md` | Step 19 |
| Access matrix | `docs-local\design\app{n}\access-matrix.yaml` | Step 17 |
| Threat model | `docs-local\design\app{n}\threat-model.md` | Step 17 |
| Domain map | `pdlf-outputs\b16\{slug}-b16-{run}-domain-map.*` | Step 17 |
| Step Receipt | `pdlf-outputs\b16\{slug}-b16-{run}-receipt.md` | Step 17 |

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `16` |
| `step_type` | `gate` |
| `skill_family` | `matt-skills` |
| `run` | From the entry record: `app1`, `app5` or the feature slug |
| `app_number` | From the entry record: 1 or 5 |
| `status` | `complete` after the gate passes; `blocked` when David says no |
| `synthesized` | `false` |
| `artifact_path` | `docs-local\GLOSSARY.md` |
| `inputs_used` | Step 15 |
| `gates` row | `gate_name = 'domain-locked'`, `step_id` = this step's row, `passed = true`, `approved_at` = the time of David's yes |
