---
title: "f46-config"
doc-id: "mb-652cce5f"
updated: "2026-11-13"
---
# Step 46 — Learning: Configuration

The fixed values of Step 46. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-f-ship-and-monitor/f46-reference|Step 46 Reference]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f46-reference.md). What the step is and why: [[[pdlf:app-factory/phase-f-ship-and-monitor/f46-explainer|Step 46 Explainer]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f46-explainer.md). What it must prove: [[[pdlf:app-factory/phase-f-ship-and-monitor/f46-test-spec|Step 46 Test Specification]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f46-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 46, Learning |
| Phase | F, Ship and Monitor |
| Carried out by | OpenCode, with the skills below; David approves lessons and answers the gate |
| Runs for | App 1 and App 5 runs, and every release |
| Previous step | 45 |
| Next step | None: the run is finished |
| Gate | `released` ([[[pdlf:pdlf-library/specifications-local/spec-gate-procedure\|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md)) |
| BFT level | Full (gate) |
| Sentinel scrutiny | None |
| Conditional | No |

## Inputs

| Input | Where |
|---|---|
| Ledger | The run's `steps`, `deviations`, `triage_findings` and `bft_records` rows |
| Receipts | `{slug}-project-library\pdlf-outputs\` |
| Repositories' history | The app and the project library |

## Where a lesson goes

| A lesson about | Goes into |
|---|---|
| The app: its features, data, screens, terms | Its project library |
| A PDLF step | That step's files in PDLF |
| A global standard, method or test | `project-library-global` |
| A skill | That skill's repository and its documentation |

## Gate summary block

```
██████████████████████████████████████████████
█  GATE — released
█
█  Step: 46   Run: {run}   BFT: Full — all six passed
█  Lessons: {n} written into their sources; {n} submitted to GBrain
█
█  Close this build cycle? (yes/no)
██████████████████████████████████████████████
```

## Outputs

| Output | Where |
|---|---|
| Retrospective | `pdlf-outputs\f46\{slug}-f46-{run}-retro.md`: each lesson, where it was written and its GBrain submission |
| Ledger | the Step 46 `steps` row; the `gates` row of `released`; its BFT record |
| Test results | `pdlf-outputs\f46\{slug}-f46-{run}-checks.xml` |
| Step Receipt | `pdlf-outputs\f46\{slug}-f46-{run}-receipt.md` |

All paths without a repository name are inside `{slug}-project-library\`.

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `46` |
| `step_type` | `gate` |
| `skill_family` | `gstack` |
| `run` | From the entry record |
| `ticket` | Empty |
| `app_number` | From the entry record |
| `status` | `complete` after the gate passes |
| `synthesized` | `false` |
| `artifact_path` | `pdlf-outputs\f46\{slug}-f46-{run}-retro.md` |
| `inputs_used` | Step 45 |
| `gates` row | Written by David with `bash /mnt/c/mybizz/scripts/pdlf-gate.sh {slug} released {run}`; the agent only reads it |
