---
title: "d32-config"
doc-id: "mb-a141bf99"
updated: "2026-11-12"
---
# Step 32 — Create the Scaffold: Configuration

The fixed values of Step 32. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d32-reference|Step 32 Reference]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d32-reference.md). What the step is and why: [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d32-explainer|Step 32 Explainer]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d32-explainer.md). What it must prove: [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d32-test-spec|Step 32 Test Specification]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d32-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 32, Create the scaffold |
| Phase | D, Scaffold and Assemble |
| Carried out by | OpenCode, with the skills below; David commits and pushes |
| Runs for | Every run that reached Step 31 |
| Previous step | 31 |
| Next step | 33 |
| Gate | None |
| BFT level | Light |
| Sentinel scrutiny | None; Step 34 reviews the structure at Very High |
| Conditional | No |

## Inputs

| Input | Where |
|---|---|
| Scaffold specification | `{slug}-project-library\docs-standard-local\scaffold-spec.md` |
| Scanner settings | `{slug}-project-library\pdlf-outputs\d31\{slug}-d31-{run}-scanner-settings.yaml` |
| Disposition list, existing app | `{slug}-project-library\pdlf-outputs\d31\{slug}-d31-{run}-disposition.md` |
| The app | `C:\dev\dev-{slug}\{slug}-app{n}` |

## Stub form

| Part | Form |
|---|---|
| Server function | `@anvil.server.callable` with the planned access decorator, and the rate-limit marker where planned |
| Docstring | One line: the behaviour and the test ID |
| Body | `raise NotImplementedError("{function}: {test ID}")` |

## Command David runs

| When | Where | Command |
|---|---|---|
| After the stubs pass their checks | WSL terminal | `cd /mnt/c/dev/dev-{slug}/{slug}-app{n} && git pull && gcp` |

## Outputs

| Output | Where |
|---|---|
| Stubs | `{slug}-app{n}\client_code\`, `server_code\` |
| Scanner configuration | `{slug}-app{n}\tests\ts-config.yaml` |
| Stub list | `pdlf-outputs\d32\{slug}-d32-{run}-stubs.md`: every module and function created |
| Test results | `pdlf-outputs\d32\{slug}-d32-{run}-checks.xml`; the scanner report `{slug}-d32-{run}-ts-scan.xml` |
| Step Receipt | `pdlf-outputs\d32\{slug}-d32-{run}-receipt.md` |
| Ledger | the Step 32 `steps` row; its BFT record |

All paths without a repository name are inside `{slug}-project-library\`.

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `32` |
| `step_type` | `skill` |
| `skill_family` | `anvil` |
| `run` | From the entry record |
| `app_number` | From the entry record |
| `status` | `complete` after David confirms the push |
| `synthesized` | `false` |
| `artifact_path` | `{slug}-app{n}` |
| `inputs_used` | Step 31 |
