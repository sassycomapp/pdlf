---
title: "e39-config"
doc-id: "mb-a9424736"
updated: "2026-11-13"
---
# Step 39 — Triage: Configuration

The fixed values of Step 39. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-e-build-and-verify/e39-reference|Step 39 Reference]]](C:/pdlf/app-factory/phase-e-build-and-verify/e39-reference.md). What the step is and why: [[[pdlf:app-factory/phase-e-build-and-verify/e39-explainer|Step 39 Explainer]]](C:/pdlf/app-factory/phase-e-build-and-verify/e39-explainer.md). What it must prove: [[[pdlf:app-factory/phase-e-build-and-verify/e39-test-spec|Step 39 Test Specification]]](C:/pdlf/app-factory/phase-e-build-and-verify/e39-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 39, Triage |
| Phase | E, Build and Verify |
| Carried out by | OpenCode, with `triage`; David decides findings and answers the gate |
| Runs for | Every ticket of the run, once each, in build order |
| Previous step | 38A |
| Next step | 35 of the next ticket; after the last ticket, 41 |
| Gate | `build-verified`, for this ticket ([[[pdlf:pdlf-library/specifications-local/spec-gate-procedure\|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md)) |
| BFT level | Full (gate) |
| Sentinel scrutiny | None; Sentinel's findings of Steps 35, 37 and 38 are triaged here |
| Conditional | No |

## Inputs

| Input | Where |
|---|---|
| Findings | `{slug}-project-library\pdlf-outputs\e35a\` to `e38a\`, the ticket's files; `triage_findings` for the ticket |
| Label vocabulary | `{slug}-project-library\docs\agents\triage-labels.md` |
| Ticket | `{slug}-project-library\pdlf-tickets\{run}\{ticket}.md` |
| Rework list | `{slug}-project-library\pdlf-outputs\d34\{slug}-d34-{run}-rework.md` |

## Gate summary block

```
██████████████████████████████████████████████
█  GATE — build-verified
█
█  Step: 39   Run: {run}   Ticket: {ticket}   BFT: Full — all six passed
█  Findings: {n} fixed, {n} declined, 0 open
█  Suite: passing; receipts of 35 to 38A match their evidence
█
█  Lock this feature and start the next? (yes/no)
██████████████████████████████████████████████
```

## Outputs

| Output | Where |
|---|---|
| Triage record | `pdlf-outputs\e39\{slug}-e39-{run}-{ticket}-triage.md`: each finding, its label and its decision |
| Ticket and rework list | `pdlf-tickets\{run}\{ticket}.md` closed; its rework items marked cleared |
| Ledger | the Step 39 `steps` row for the ticket; the `gates` row of `build-verified`; its BFT record |
| Test results | `pdlf-outputs\e39\{slug}-e39-{run}-{ticket}-checks.xml` |
| Step Receipt | `pdlf-outputs\e39\{slug}-e39-{run}-{ticket}-receipt.md` |

All paths without a repository name are inside `{slug}-project-library\`.

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `39` |
| `step_type` | `gate` |
| `skill_family` | `matt-skills` |
| `run` | From the entry record |
| `ticket` | The ticket's slug |
| `app_number` | From the entry record |
| `status` | `complete` after the gate passes; `blocked` when David says no |
| `synthesized` | `false` |
| `artifact_path` | `pdlf-outputs\e39\{slug}-e39-{run}-{ticket}-triage.md` |
| `inputs_used` | Steps 35 to 38A |
| `gates` row | Written by David with `bash /mnt/c/mybizz/scripts/pdlf-gate.sh {slug} build-verified {run} {ticket}`; the agent only reads it |
