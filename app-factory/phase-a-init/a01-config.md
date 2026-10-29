---
title: "a01-config"
doc-id: "mb-0aff45b8"
updated: "2026-10-29"
---
# Step 1 — Orchestrator: Configuration

The fixed values of Step 1. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-a-init/a01-reference|Step 1 Reference]]](C:/pdlf/app-factory/phase-a-init/a01-reference.md). What the step is and why: [[[pdlf:app-factory/phase-a-init/a01-explainer|Step 1 Explainer]]](C:/pdlf/app-factory/phase-a-init/a01-explainer.md). What it must prove: [[[pdlf:app-factory/phase-a-init/a01-test-spec|Step 1 Test Specification]]](C:/pdlf/app-factory/phase-a-init/a01-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 1, Orchestrator |
| Phase | A, Init |
| Carried out by | OpenCode's Build agent, through the skill `pdlf-init` |
| Started by | David, with `/pdlf-init` |
| Gate | None of its own; it stops at every gate of the steps it runs |
| BFT level | None for itself; each step at its own level; every gate Full |
| Sentinel scrutiny | None for itself; each step at its own scrutiny |

## Where it runs

| Item | Value |
|---|---|
| OpenCode opened in | The business folder, `C:\dev\dev-{slug}\`, through its link in the home folder, `/home/dev-p/projects/dev-{slug}`, because the OpenCode web UI opens only folders inside `/home/dev-p` |
| The link | One line in `/etc/fstab`: `/mnt/c/dev/dev-{slug} /home/dev-p/projects/dev-{slug} none bind,nofail 0 0` |
| The working folder | The folder OpenCode was opened in. Every file of the business is written through it: `{working folder}/{slug}-project-library/...`, `{working folder}/{slug}-app{n}/...`. A path under `/mnt/c/dev/dev-{slug}` names the same file, but Cupcake treats it as another project and blocks the write |
| The slug | The business folder's name without `dev-`: lowercase letters, digits and hyphens only |
| A new business | David creates the empty folder `C:\dev\dev-{slug}\` and its link first, then opens OpenCode in it |
| PDLF | `/mnt/c/pdlf`, read only |
| OpenCode configuration | The global configuration, the global `AGENTS.md` and Cupcake; PDLF has no `opencode.json` of its own |
| Skill source | `C:\pdlf\pdlf-library\skills-local\pdlf-init\SKILL.md` |
| Skill installed | `~/.config/opencode/skills/pdlf-init/SKILL.md` |
| David's install command | `mkdir -p ~/.config/opencode/skills/pdlf-init && cp /mnt/c/pdlf/pdlf-library/skills-local/pdlf-init/SKILL.md ~/.config/opencode/skills/pdlf-init/SKILL.md` |
| Ledger | Database `pdlf`, port 5433, through the PowerShell bridge ([[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger\|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md)) |

## The built phases

The orchestrator runs only the steps of these phases. A run that reaches a step of any other phase pauses there.

| Phase | Steps | Built |
|---|---|---|
| A, Init | 1 to 10 | Yes |
| B, Discover and Define | 11, 12, 14, 15, 16 | Yes |
| C, Design and Plan | 17 to 23, 26 to 28 | No |
| D, Scaffold and Assemble | 29 to 34 | No |
| E, Build and Verify | 35, 35A, 40, 40B, 36, 37, 38, 38A, 39 | No |
| F, Ship and Monitor | 41, 42, 42A, 43 to 46 | No |

## The entry points

| Entry | Name | App | Run | Health check first | Route |
|---|---|---|---|---|---|
| 02 | `new-app-no-context` | 1 | `app1` | No | Application |
| 03 | `new-app-with-context` | 1 | `app1` | No | Application |
| 04 | `add-feature-main-app` | 1 | the feature slug | Yes | Feature |
| 05 | `update-main-app` | 1 | the update slug | Yes | Feature, when the update changes what the app does; otherwise Update |
| 06 | `compile-master-template` | 2 | `app2` | Yes | Release |
| 07 | `create-client-template` | 3 | `app3` | Yes | Client template |
| 08 | `create-management-app` | 5 | `app5` | Yes | Management app |
| 09 | `add-feature-management-app` | 3 or 5 | the feature slug | Yes | Feature |
| 10 | `update-management-app` | 3 or 5 | the update slug | Yes | Feature, when the update changes what the app does; otherwise Update |

Each entry point's questions and values are in its own configuration, `a{nn}-config.md`.

## The routes

Every run follows one route: its steps, in this order. A phase not yet built is listed by its name only; its steps are added here when it is built.

| Route | Steps, in order |
|---|---|
| Application | 11, 12, 14, 15, 16 (gate `domain-locked`), then Phases C to F |
| Management app | 11, 12, 14, 15, 16 (gate `domain-locked`), then Phases C to F |
| Client template | 11, then Phase G |
| Feature | 12, 14, 15, 16 (gate `domain-locked`), then Phases C to F |
| Update | The step David names at the entry, then every later step of the Application route |
| Release | Phase F: 41, 42, 42A, 43, 44 |

## The dependencies

A step runs only when every step it depends on is `complete` or `skipped`, and every gate before it in the route is passed for the run.

| Step | Depends on |
|---|---|
| 11 | The run's entry-point row |
| 12 | Step 11 of the app worked on (run `app{n}`); for a Feature or Update run, also the gate `domain-locked` passed for that app's run `app{n}` |
| 14 | Step 12 of the run |
| 15 | Steps 12 and 14 of the run |
| 16 | Step 15 of the run |

## The gates in the built phases

| Gate | At step | David's command |
|---|---|---|
| `domain-locked` | 16 | `bash /mnt/c/mybizz/scripts/pdlf-gate.sh {slug} domain-locked {run}` |

## The resume check

| Ledger state of a run | What the orchestrator does |
|---|---|
| The entry row is `complete`, and a step of the route has no row, or a row that is not `complete` or `skipped` | Unfinished: offer to continue it at the first such step |
| That step's row is `in_progress` | Offer to start that step again from its beginning; files an earlier attempt wrote are kept and checked, never overwritten without David's permission |
| That step's row is `blocked` | Present its `blockers` as a deviation; David decides |
| That step's phase is not built | Paused: report the run and the step; do not offer it |
| Every step of the route is `complete` or `skipped` | Finished: not offered |

## The entry record

Written by the entry point into the `inputs_used` of its own `steps` row, as JSON. Every step of the run reads it from there.

| Field | Value |
|---|---|
| `entry_point` | `02` to `10` |
| `route` | `application`, `management-app`, `client-template`, `feature`, `update` or `release` |
| `app_number` | 1, 2, 3 or 5 |
| `run` | `app1`, `app2`, `app3`, `app5`, or the feature or update slug |
| `statement` | For a feature or an update: David's statement of it, in his words; otherwise `null` |
| `start_step` | For an Update run: the step David names; otherwise the route's first step |
| `fault` | For an update: `true` when it corrects a fault; otherwise `false` |
| `existing_apps` | For entries 03, 07 and 08: the app numbers that already exist; otherwise `null` |
| `project_context` | For entry 03: `{slug}-project-context` when the business's existing project library holds its context; otherwise `null` |
| `reference_platform` | For entry 03: the reference platform's name and where its material is kept now; otherwise `null` |

## Ledger values

| Row | Column | Value |
|---|---|---|
| `projects` (entries 02 and 03) | `slug`, `project_name`, `mode` | The slug from the folder; the name and the mode (`full` or `test`) from David |
| Entry-point `steps` row | `step_number` | `02` to `10` |
| | `sort_order` | 2 to 10 |
| | `phase` | `A` |
| | `run`, `app_number` | From the entry record |
| | `step_type` | `skill` |
| | `skill_family` | `opencode` |
| | `skill_name` | `pdlf-init` |
| | `inputs_used` | The entry record |
| | `status` | `complete` |
| | `artifact_path` | `pdlf-outputs\a{nn}\{slug}-a{nn}-{run}-receipt.md` |

## Outputs of an entry point

| Output | Where |
|---|---|
| Health check report (entries 04 to 10) | `{slug}-project-library\pdlf-outputs\a{nn}\{slug}-a{nn}-{run}-health-check.md` |
| Test results | `{slug}-project-library\pdlf-outputs\a{nn}\{slug}-a{nn}-{run}-checks.xml` (JUnit XML, `ts-method` section 5) |
| Step Receipt | `{slug}-project-library\pdlf-outputs\a{nn}\{slug}-a{nn}-{run}-receipt.md` |

For entries 02 and 03 the project library does not exist yet when the entry is taken: Step 11 writes their receipt and test results from the entry row once it has made the library.

## Skills and tools

| Skill or tool | Used for |
|---|---|
| `pdlf-init` | Starting the orchestrator |
| [[[pdlf:pdlf-library/operating-procedures/sop-health-check\|SOP: Health Check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md) | The health check of entries 04 to 10 |
| `writing-for-agents` | Writing or changing `pdlf-init`'s `SKILL.md` |
| `pdlf-gate.sh` | David's record of a gate's approval; never run by the agent |
