---
title: "c26-config"
doc-id: "mb-b69a9094"
updated: "2026-11-12"
---
# Step 26 — Screens Approved: Configuration

The fixed values of Step 26. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-c-design-and-plan/c26-reference|Step 26 Reference]]](C:/pdlf/app-factory/phase-c-design-and-plan/c26-reference.md). What the step is and why: [[[pdlf:app-factory/phase-c-design-and-plan/c26-explainer|Step 26 Explainer]]](C:/pdlf/app-factory/phase-c-design-and-plan/c26-explainer.md). What it must prove: [[[pdlf:app-factory/phase-c-design-and-plan/c26-test-spec|Step 26 Test Specification]]](C:/pdlf/app-factory/phase-c-design-and-plan/c26-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 26, Screens approved |
| Phase | C, Design and Plan; the last step of the phase |
| Carried out by | OpenCode; David decides findings, approves each screen requirement and answers the gate |
| Runs for | Every run that reached Step 23 |
| Previous step | 23 (Steps 24 and 25 are not used) |
| Next step | 31, the first step of Phase D (Steps 27 to 30 are not used) |
| Gate | `screens-approved` ([[[pdlf:pdlf-library/specifications-local/spec-gate-procedure\|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md)) |
| BFT level | Full (gate) |
| Sentinel scrutiny | None; Step 22's review covers the same documents |
| Conditional | No |

## Inputs

| Input | Where |
|---|---|
| Screen requirements and index | `{slug}-project-library\ui\`; `pdlf-outputs\c22\{slug}-c22-{run}-requirement-index.md` |
| Design review | `{slug}-project-library\pdlf-outputs\c23\{slug}-c23-{run}-design-review.md` |
| Design system | `{slug}-project-library\docs-local\DESIGN.md` |
| Receipts of Steps 21 to 23 | `{slug}-project-library\pdlf-outputs\c21\` to `c23\` |

## Finding outcomes

| Finding | Allowed outcomes |
|---|---|
| Theme usage | Corrected: the better-fitting component replaces the plainer one |
| Other high | Corrected |
| Medium or low | Corrected, or declined by David with his reason |

## Outputs

| Output | Where |
|---|---|
| Screen requirements | `ui\<package path>\<FormName>\<FormName>-requirement.md`, `status: approved` |
| Finding outcomes | `pdlf-outputs\c26\{slug}-c26-{run}-findings.md`: each finding of Step 23 with its outcome and, for a declined one, David's reason |
| Step-folder copies | `pdlf-outputs\c26\{slug}-c26-{run}-requirement-{module path}.md` for each approved requirement |
| Test results | `pdlf-outputs\c26\{slug}-c26-{run}-checks.xml` |
| Step Receipt | `pdlf-outputs\c26\{slug}-c26-{run}-receipt.md` |
| Ledger | the Step 26 `steps` row; the `gates` row of `screens-approved`; its BFT record |

All paths are inside `{slug}-project-library\`.

## Gate summary block

```
██████████████████████████████████████████████
█  GATE — screens-approved
█
█  Step: 26   Run: {run}   BFT: Full — all six passed
█  Screen requirements approved: {n} of {n}
█  Findings: {n} corrected, {n} declined, 0 open
█  Locks: every screen requirement; Phase C is closed
█
█  Proceed to Phase D? (yes/no)
██████████████████████████████████████████████
```

## Hand-over to Phase D

| Item | Where |
|---|---|
| Approved screen requirements | `ui\` |
| Requirement index | `pdlf-outputs\c22\{slug}-c22-{run}-requirement-index.md` |
| Access matrix | `docs-local\design\app{n}\access-matrix.yaml` |
| Design system | `docs-local\DESIGN.md` |
| Tickets | `pdlf-tickets\{run}\` |
| Step Receipt | `pdlf-outputs\c26\{slug}-c26-{run}-receipt.md` |

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `26` |
| `step_type` | `gate` |
| `skill_family` | `opencode` |
| `run` | From the entry record |
| `app_number` | From the entry record |
| `status` | `complete` after the gate passes; `blocked` when David says no |
| `synthesized` | `false` |
| `artifact_path` | `ui\` |
| `inputs_used` | Steps 22 and 23 |
| `gates` row | Written by David with `bash /mnt/c/mybizz/scripts/pdlf-gate.sh {slug} screens-approved {run}`; the agent only reads it |
