---
title: "f41-config"
doc-id: "mb-dccc0401"
updated: "2026-11-13"
---
# Step 41 — Release Readiness: Configuration

The fixed values of Step 41. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-f-ship-and-monitor/f41-reference|Step 41 Reference]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f41-reference.md). What the step is and why: [[[pdlf:app-factory/phase-f-ship-and-monitor/f41-explainer|Step 41 Explainer]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f41-explainer.md). What it must prove: [[[pdlf:app-factory/phase-f-ship-and-monitor/f41-test-spec|Step 41 Test Specification]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f41-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 41, Release Readiness |
| Phase | F, Ship and Monitor |
| Carried out by | OpenCode, with the skills below; David commits, tags and pushes |
| Runs for | App 1 and App 5 runs, and every release |
| Previous step | 39 of the last ticket |
| Next step | 42 |
| Gate | None |
| BFT level | Full |
| Sentinel scrutiny | None; Sentinel reviewed every feature in Phase E |
| Conditional | No; first-release checks only at a first release |

## Inputs

| Input | Where |
|---|---|
| Tickets and gates | `{slug}-project-library\pdlf-tickets\{run}\`; the `gates` rows of `build-verified` |
| Test plan | `{slug}-project-library\docs-local\design\{run}\test-plan.md` |
| Assessment plan | Step 15's threat model, `{slug}-project-library\docs-local\design\app{n}\threat-model.md` |
| Schema migration log | `{slug}-project-library\docs-local\schema-migration-log.md` |
| The app | `C:\dev\dev-{slug}\{slug}-app{n}` |

## First-release checks

| Check | Pass when |
|---|---|
| Legal documents | Privacy Policy, Terms of Service and Cookie Policy exist (DC-14) |
| Exit export, App 1 | The test client's data lands complete in its bucket (RL-08) |
| Legal documents system, App 1 | `spec-legal-documents-and-consent` section 12 passes on the test client instance |
| Media host | `media.mybizz.live` sets no cookie |

## Command David runs

| When | Where | Command |
|---|---|---|
| After the report is clean | WSL terminal | `cd /mnt/c/dev/dev-{slug}/{slug}-app{n} && git pull && gcp && git tag {version} && git push origin {version}` |

## Outputs

| Output | Where |
|---|---|
| Readiness report | `pdlf-outputs\f41\{slug}-f41-{run}-readiness.md` |
| Release notes | `pdlf-outputs\f41\{slug}-f41-{run}-release-notes.md` |
| Performance baseline | `pdlf-outputs\f41\{slug}-f41-{run}-benchmark.md` |
| Ledger | the Step 41 `steps` row; its BFT record |
| Test results | `pdlf-outputs\f41\{slug}-f41-{run}-checks.xml` |
| Step Receipt | `pdlf-outputs\f41\{slug}-f41-{run}-receipt.md` |

All paths without a repository name are inside `{slug}-project-library\`.

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `41` |
| `step_type` | `skill` |
| `skill_family` | `opencode` |
| `run` | From the entry record |
| `ticket` | Empty |
| `app_number` | From the entry record |
| `status` | `complete` after David's tag is pushed |
| `synthesized` | `false` |
| `artifact_path` | `pdlf-outputs\f41\{slug}-f41-{run}-readiness.md` |
| `inputs_used` | Step 39 of the last ticket |
