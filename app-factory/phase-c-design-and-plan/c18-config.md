---
title: "c18-config"
doc-id: "mb-721ae22b"
updated: "2026-11-12"
---
# Step 18 — Pull to Local: Configuration

The fixed values of Step 18. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-c-design-and-plan/c18-reference|Step 18 Reference]]](C:/pdlf/app-factory/phase-c-design-and-plan/c18-reference.md). What the step is and why: [[[pdlf:app-factory/phase-c-design-and-plan/c18-explainer|Step 18 Explainer]]](C:/pdlf/app-factory/phase-c-design-and-plan/c18-explainer.md). What it must prove: [[[pdlf:app-factory/phase-c-design-and-plan/c18-test-spec|Step 18 Test Specification]]](C:/pdlf/app-factory/phase-c-design-and-plan/c18-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 18, Pull to local |
| Phase | C, Design and Plan |
| Carried out by | David runs the pull; OpenCode checks it |
| Runs for | Every run that reached Step 17; the same procedure runs as Steps 30 and 33 |
| Previous step | 17 |
| Next step | 19 |
| Gate | None |
| BFT level | None |
| Sentinel scrutiny | None |
| Conditional | No |

## Inputs

| Input | Where |
|---|---|
| Step 17 receipt | `{slug}-project-library\pdlf-outputs\c17\{slug}-c17-{run}-receipt.md` |
| Authoritative schema | `{slug}-project-library\docs-standard-local\authoritative-schema.md` |
| The app's local repository | `C:\dev\dev-{slug}\{slug}-app{n}` |

## Command David runs

| Where | Command |
|---|---|
| WSL terminal | `cd /mnt/c/dev/dev-{slug}/{slug}-app{n} && git pull` |

## Checks

| Check | Pass when |
|---|---|
| Clean | `git status --short` prints nothing |
| Level | `git rev-parse master` equals `git rev-parse origin/master` |
| Expected change | Step 17: `db_schema` in `anvil.yaml` equals the authoritative schema. Step 30: the forms Step 29 built. Step 33: the modules and functions Step 32 created |
| Nothing else | `git diff --name-only` between the receipt's recorded commit and `master` lists only files the step before it expected, apart from formatting Anvil itself applies |
| Validates | `anvil --json validate .` reports no error |

## Outputs

| Output | Where |
|---|---|
| Test results | `pdlf-outputs\c18\{slug}-c18-{run}-checks.xml` |
| Step Receipt | `pdlf-outputs\c18\{slug}-c18-{run}-receipt.md`, recording the commit `master` now points to |
| Ledger | the Step 18 `steps` row |

All paths without a repository name are inside `{slug}-project-library\`.

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `18` |
| `step_type` | `manual` |
| `skill_family` | `manual` |
| `run` | From the entry record |
| `app_number` | From the entry record |
| `status` | `complete` when every check passes |
| `synthesized` | `false` |
| `artifact_path` | `{slug}-app{n}` |
| `inputs_used` | Step 17 |
