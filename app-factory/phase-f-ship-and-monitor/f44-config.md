---
title: "f44-config"
doc-id: "mb-1edd98fd"
updated: "2026-11-13"
---
# Step 44 — Release: Configuration

The fixed values of Step 44. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-f-ship-and-monitor/f44-reference|Step 44 Reference]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f44-reference.md). What the step is and why: [[[pdlf:app-factory/phase-f-ship-and-monitor/f44-explainer|Step 44 Explainer]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f44-explainer.md). What it must prove: [[[pdlf:app-factory/phase-f-ship-and-monitor/f44-test-spec|Step 44 Test Specification]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f44-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 44, Release |
| Phase | F, Ship and Monitor |
| Carried out by | David, at the gate; OpenCode prepares and checks |
| Runs for | App 1 and App 5 runs, and every release |
| Previous step | 43 |
| Next step | 45 |
| Gate | `production-released` ([[[pdlf:pdlf-library/specifications-local/spec-gate-procedure\|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md)) |
| BFT level | Full (gate) |
| Sentinel scrutiny | None |
| Conditional | No; the release action differs for App 1 and App 5 |

## Inputs

| Input | Where |
|---|---|
| Results of Steps 41 to 43 | `{slug}-project-library\pdlf-outputs\f41\` to `f43\` |
| Open findings | `triage_findings` for the run |

## Gate summary block

```
██████████████████████████████████████████████
█  GATE — production-released
█
█  Step: 44   Run: {run}   Release: {version}   BFT: Full — all six passed
█  Readiness: passed   Regression: passed   Test client: healthy
█  Open findings: 0
█
█  Release to every client? (yes/no)
██████████████████████████████████████████████
```

## Release stages, App 1

| Stage | Moves | Passes when |
|---|---|---|
| 1 | The test client instance | Its health check passes |
| 2 | 10% of client instances | Their health checks pass |
| 3 | Every client instance | Their health checks pass |

## Outputs

| Output | Where |
|---|---|
| Release record | `pdlf-outputs\f44\{slug}-f44-{run}-release.md`: each stage and its health check, or App 5's published version |
| Ledger | the Step 44 `steps` row; the `gates` row of `production-released`; its BFT record |
| Test results | `pdlf-outputs\f44\{slug}-f44-{run}-checks.xml` |
| Step Receipt | `pdlf-outputs\f44\{slug}-f44-{run}-receipt.md` |

All paths without a repository name are inside `{slug}-project-library\`.

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `44` |
| `step_type` | `gate` |
| `skill_family` | `manual` |
| `run` | From the entry record |
| `ticket` | Empty |
| `app_number` | From the entry record |
| `status` | `complete` after the release; `blocked` when David says no |
| `synthesized` | `false` |
| `artifact_path` | `pdlf-outputs\f44\{slug}-f44-{run}-release.md` |
| `inputs_used` | Steps 41 to 43 |
| `gates` row | Written by David with `bash /mnt/c/mybizz/scripts/pdlf-gate.sh {slug} production-released {run}`; the agent only reads it |
