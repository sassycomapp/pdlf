---
title: "c21-config"
doc-id: "mb-2cd6bb36"
updated: "2026-11-12"
---
# Step 21 — Concept Check: Configuration

The fixed values of Step 21. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-c-design-and-plan/c21-reference|Step 21 Reference]]](C:/pdlf/app-factory/phase-c-design-and-plan/c21-reference.md). What the step is and why: [[[pdlf:app-factory/phase-c-design-and-plan/c21-explainer|Step 21 Explainer]]](C:/pdlf/app-factory/phase-c-design-and-plan/c21-explainer.md). What it must prove: [[[pdlf:app-factory/phase-c-design-and-plan/c21-test-spec|Step 21 Test Specification]]](C:/pdlf/app-factory/phase-c-design-and-plan/c21-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 21, Concept check |
| Phase | C, Design and Plan |
| Carried out by | OpenCode; David resolves contradictions and answers the gate |
| Runs for | App 1 and App 5 as a whole application; every feature |
| Previous step | 20 |
| Next step | 22 |
| Gate | `concept-locked` ([[[pdlf:pdlf-library/specifications-local/spec-gate-procedure\|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md)) |
| BFT level | Full (gate) |
| Sentinel scrutiny | Medium |
| Conditional | No |

## Concept documents

| Document | Where |
|---|---|
| Reviewed plan | `docs-local\design\{run}\design-doc.md` |
| Test plan | `docs-local\design\{run}\test-plan.md` |
| Access matrix | `docs-local\design\app{n}\access-matrix.yaml` |
| Threat model | `docs-local\design\app{n}\threat-model.md` |
| Glossary | `docs-local\GLOSSARY.md` |
| ADRs | `adr-local\` |
| Authoritative schema | `docs-standard-local\authoritative-schema.md` |
| Tickets and flows | `pdlf-tickets\{run}\`; `pdlf-outputs\c19\` |
| Design system | `docs-local\DESIGN.md` |

All paths are inside `{slug}-project-library\`.

## Fixed checks

| Check | Pass when |
|---|---|
| Tables | Every table a ticket names exists in the authoritative schema |
| Access | Every server function and form a ticket names is in the access matrix, or is listed for Step 22 to add |
| Terms | Every term in the tickets and `DESIGN.md` is the glossary's term |
| Tests | Every test ID a ticket names exists in the test plan |
| Decisions | Every ADR is followed by the documents it governs |
| Receipts | `ts_report.py {step folder} --prefix {slug}-{step}-{run}- --check {receipt}` passes for c17, c18, c19 and c20 (c20 is skipped when David skipped Step 20) |

## Outputs

| Output | Where |
|---|---|
| Concept check report | `pdlf-outputs\c21\{slug}-c21-{run}-concept-check.md`: each pair, what was compared, each contradiction and its correction, the verdict |
| Test results | `pdlf-outputs\c21\{slug}-c21-{run}-checks.xml` |
| Step Receipt | `pdlf-outputs\c21\{slug}-c21-{run}-receipt.md` |
| Ledger | the Step 21 `steps` row; the `gates` row of `concept-locked`; its BFT record; its `triage_findings` row |

## Gate summary block

```
██████████████████████████████████████████████
█  GATE — concept-locked
█
█  Step: 21   Run: {run}   BFT: Full — all six passed
█  Concept check: {n} pairs checked, {n} contradictions resolved
█  Locks: the plan, the tickets, the schema, DESIGN.md,
█         the access matrix, the threat model
█
█  Proceed to the screen requirements? (yes/no)
██████████████████████████████████████████████
```

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `21` |
| `step_type` | `gate` |
| `skill_family` | `opencode` |
| `run` | From the entry record |
| `app_number` | From the entry record |
| `status` | `complete` after the gate passes; `blocked` when David says no |
| `synthesized` | `false` |
| `artifact_path` | `pdlf-outputs\c21\{slug}-c21-{run}-concept-check.md` |
| `inputs_used` | Steps 16 to 20 |
| `gates` row | Written by David with `bash /mnt/c/mybizz/scripts/pdlf-gate.sh {slug} concept-locked {run}`; the agent only reads it |
