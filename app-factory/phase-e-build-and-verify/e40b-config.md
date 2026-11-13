---
title: "e40b-config"
doc-id: "mb-25f93005"
updated: "2026-11-13"
---
# Step 40B — Approved Fixes: Configuration

The fixed values of Step 40B. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-e-build-and-verify/e40b-reference|Step 40B Reference]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40b-reference.md). What the step is and why: [[[pdlf:app-factory/phase-e-build-and-verify/e40b-explainer|Step 40B Explainer]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40b-explainer.md). What it must prove: [[[pdlf:app-factory/phase-e-build-and-verify/e40b-test-spec|Step 40B Test Specification]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40b-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 40B, Approved Fixes |
| Phase | E, Build and Verify |
| Carried out by | OpenCode, with the skills below; David commits |
| Runs for | Every ticket of the run, once each, in build order |
| Previous step | 40 |
| Next step | 36 |
| Gate | None |
| BFT level | Light |
| Sentinel scrutiny | None |
| Conditional | Yes; skipped when Step 40 was skipped or David approved no fix |

## Inputs

| Input | Where |
|---|---|
| Scan report | `{slug}-project-library\pdlf-outputs\e40\{slug}-e40-{run}-{ticket}-scan.md` |
| The app | `C:\dev\dev-{slug}\{slug}-app{n}` |

## Command David runs

| When | Where | Command |
|---|---|---|
| After the fixes pass | WSL terminal | `cd /mnt/c/dev/dev-{slug}/{slug}-app{n} && git pull && gcp` |

## Outputs

| Output | Where |
|---|---|
| Fixes | `{slug}-app{n}` |
| Ledger | the Step 40B `steps` row for the ticket; its BFT record |
| Test results | `pdlf-outputs\e40b\{slug}-e40b-{run}-{ticket}-checks.xml` |
| Step Receipt | `pdlf-outputs\e40b\{slug}-e40b-{run}-{ticket}-receipt.md` |

All paths without a repository name are inside `{slug}-project-library\`.

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `40B` |
| `step_type` | `optional` |
| `skill_family` | `opencode` |
| `run` | From the entry record |
| `ticket` | The ticket's slug |
| `app_number` | From the entry record |
| `status` | `complete`, or `skipped` when there is nothing to fix |
| `synthesized` | `false` |
| `artifact_path` | `{slug}-app{n}` |
| `inputs_used` | Step 40 |
