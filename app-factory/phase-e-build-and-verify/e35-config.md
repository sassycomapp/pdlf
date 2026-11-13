---
title: "e35-config"
doc-id: "mb-d062d332"
updated: "2026-11-13"
---
# Step 35 — Build: Configuration

The fixed values of Step 35. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-e-build-and-verify/e35-reference|Step 35 Reference]]](C:/pdlf/app-factory/phase-e-build-and-verify/e35-reference.md). What the step is and why: [[[pdlf:app-factory/phase-e-build-and-verify/e35-explainer|Step 35 Explainer]]](C:/pdlf/app-factory/phase-e-build-and-verify/e35-explainer.md). What it must prove: [[[pdlf:app-factory/phase-e-build-and-verify/e35-test-spec|Step 35 Test Specification]]](C:/pdlf/app-factory/phase-e-build-and-verify/e35-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 35, Build |
| Phase | E, Build and Verify |
| Carried out by | OpenCode, with the skills below; Anvil's agent wires; Claude reviews through David; David commits and signs off |
| Runs for | Every ticket of the run, once each, in build order |
| Previous step | 34 (gate `architecture-verified`), or 39 of the previous ticket |
| Next step | 35A |
| Gate | None |
| BFT level | Full |
| Sentinel scrutiny | High |
| Conditional | No; old forms and rework items only where the ticket has them |

## Inputs

| Input | Where |
|---|---|
| Ticket | `{slug}-project-library\pdlf-tickets\{run}\{ticket}.md` |
| Scaffold specification | `{slug}-project-library\docs-standard-local\scaffold-spec.md` |
| Approved screen requirements | `{slug}-project-library\ui\`, the ticket's forms |
| Authoritative schema and SRS | `{slug}-project-library\docs-standard-local\` |
| Access matrix and threat model | `{slug}-project-library\docs-local\design\app{n}\` |
| Test plan | `{slug}-project-library\docs-local\design\{run}\test-plan.md` |
| Rework and disposition lists | `{slug}-project-library\pdlf-outputs\d34\`; `pdlf-outputs\d31\` |
| The app | `C:\dev\dev-{slug}\{slug}-app{n}` |

## Order of work

| # | Who | Work | `mo-ui-production` section 4 |
|---|---|---|---|
| 1 | OpenCode | Check the ticket, its screen requirements, the schema and the SRS agree | step 1 |
| 2 | OpenCode | Server code test-first into the stubs; Levels 0, 1 and 2 | step 2 |
| 3 | Claude, through David | Review the server code against the screen requirements and the SRS | step 3 |
| 4 | David | Commit the documentation repositories and the app | step 4 |
| 5 | OpenCode | `mb-form-builder` for the ticket's forms; old forms removed | step 5 |
| 6 | Claude, through David | Review each form and spec sheet | step 6 |
| 7 | David | Commit; open each form in Anvil | steps 7 and 8 |
| 8 | David, Anvil's agent | Wiring task; `/review-commit` | steps 9 and 10 |
| 9 | David, OpenCode | Pull; `anvil --json validate`, `ts_scan.py` | step 11 |
| 10 | Claude, through David | Confirm only handler bodies changed | step 12 |
| 11 | OpenCode, David | Rework items cleared; Level 3 in the browser; sign-off | steps 13 and 14 |

## Commands David runs

| When | Where | Command |
|---|---|---|
| Each commit of the app | WSL terminal | `cd /mnt/c/dev/dev-{slug}/{slug}-app{n} && git pull && gcp` |
| Each commit of the documentation | WSL terminal | `cd /mnt/c/mybizz/scripts && bash commit-all.sh "{message}"` |
| Before Level 2 | WSL terminal | `bash /mnt/c/dev/project-library-global/test-suite/tools/ts_local.sh /mnt/c/dev/dev-{slug}/{slug}-app{n} start` |

## Outputs

| Output | Where |
|---|---|
| Feature code, forms, spec sheets, tests | `{slug}-app{n}\client_code\`, `server_code\`, `theme\assets\docs\app{n}\`, `tests\` |
| Access matrix and phrase keys | `docs-local\design\app{n}\access-matrix.yaml`; `{slug}-app{n}\client_code\shared\translations\en.py` |
| Review notes | `pdlf-outputs\e35\{slug}-e35-{run}-{ticket}-reviews.md`: each of Claude's three reviews and its outcome |
| Ledger | the Step 35 `steps` row for the ticket; its BFT record; its `triage_findings` row |
| Test results | `pdlf-outputs\e35\{slug}-e35-{run}-{ticket}-checks.xml` |
| Step Receipt | `pdlf-outputs\e35\{slug}-e35-{run}-{ticket}-receipt.md` |

All paths without a repository name are inside `{slug}-project-library\`.

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `35` |
| `step_type` | `skill` |
| `skill_family` | `opencode` |
| `run` | From the entry record |
| `ticket` | The ticket's slug |
| `app_number` | From the entry record |
| `status` | `complete` after David signs the feature off |
| `synthesized` | `false` |
| `artifact_path` | `{slug}-app{n}` |
| `inputs_used` | Step 34, or Step 39 of the previous ticket |
