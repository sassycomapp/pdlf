---
title: "c17-config"
doc-id: "mb-536f2e3d"
updated: "2026-11-12"
---
# Step 17 — Create Anvil Data Tables: Configuration

The fixed values of Step 17. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-c-design-and-plan/c17-reference|Step 17 Reference]]](C:/pdlf/app-factory/phase-c-design-and-plan/c17-reference.md). What the step is and why: [[[pdlf:app-factory/phase-c-design-and-plan/c17-explainer|Step 17 Explainer]]](C:/pdlf/app-factory/phase-c-design-and-plan/c17-explainer.md). What it must prove: [[[pdlf:app-factory/phase-c-design-and-plan/c17-test-spec|Step 17 Test Specification]]](C:/pdlf/app-factory/phase-c-design-and-plan/c17-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 17, Create Anvil data tables |
| Phase | C, Design and Plan; the first step of the phase |
| Carried out by | OpenCode, with the skills below; David renames, commits and applies |
| Runs for | App 1 and App 5 as a whole application; every feature that adds or changes tables |
| Previous step | 16 |
| Next step | 18 |
| Gate | None |
| BFT level | Light |
| Sentinel scrutiny | High |
| Conditional | No; the authoritative schema is written only when it is empty; renames and removals occur only when the difference list has them |

## Inputs

| Input | Where |
|---|---|
| Reviewed plan, with the data design | `{slug}-project-library\docs-local\design\{run}\design-doc.md` |
| Glossary | `{slug}-project-library\docs-local\GLOSSARY.md` |
| ADRs | `{slug}-project-library\adr-local\` |
| Access matrix and threat model | `{slug}-project-library\docs-local\design\app{n}\` |
| Domain map | `{slug}-project-library\pdlf-outputs\b16\{slug}-b16-{run}-domain-map.*` |
| Step 16 receipt | `{slug}-project-library\pdlf-outputs\b16\{slug}-b16-{run}-receipt.md` |
| Authoritative schema | `{slug}-project-library\docs-standard-local\authoritative-schema.md` |
| Schema migration log | `{slug}-project-library\docs-local\schema-migration-log.md` |
| The app's schema | `C:\dev\dev-{slug}\{slug}-app{n}\anvil.yaml`, `db_schema` |
| The app's test copies | `C:\dev\dev-{slug}\{slug}-app{n}\tests\ts-config.yaml` and `tests\component-inventory.yaml` |
| Theme inventory | `C:\dev\dev-m3-custom-theme\m3-custom-theme-project-library\docs\component-inventory.yaml` |
| Test configuration template | `C:\dev\project-library-global\test-suite\templates\ts-config.yaml` |
| Context pack | [[[pdlf:pdlf-library/specifications-local/spec-skill-context-pack\|Spec: Skill Context Pack]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-context-pack.md) |

## Outputs

| Output | Where |
|---|---|
| Authoritative schema, when it was empty | `docs-standard-local\authoritative-schema.md`, in the structure the project template gives the file |
| Schema difference list | `pdlf-outputs\c17\{slug}-c17-{run}-schema-diff.md`: additions, renames and removals, table by table |
| David's instructions | `pdlf-outputs\c17\{slug}-c17-{run}-instructions.md`, written with `wizard` |
| App schema | `{slug}-app{n}\anvil.yaml`, `db_schema` |
| App test copies | `{slug}-app{n}\tests\component-inventory.yaml`, equal to the theme's; the theme keys of `{slug}-app{n}\tests\ts-config.yaml`, equal to the template's |
| Migration log rows | `docs-local\schema-migration-log.md`, one row per change, with its migration plan |
| Step-folder copies | `pdlf-outputs\c17\{slug}-c17-{run}-authoritative-schema.md`; `-anvil-db-schema.yaml` (the `db_schema` section) |
| Test results | `pdlf-outputs\c17\{slug}-c17-{run}-checks.xml` (JUnit XML, ts-method section 5); the scanner report `{slug}-c17-{run}-ts-scan.xml` |
| Step Receipt | `pdlf-outputs\c17\{slug}-c17-{run}-receipt.md` |
| Ledger | the Step 17 `steps` row; its BFT record; its `triage_findings` row |

All paths without a repository name are inside `{slug}-project-library\`.

## Schema rules

| Rule | Source |
|---|---|
| Every table refuses client access: `client: none` | `spec-anvil-platform-standards` section 10; `data-models` |
| Every table has `created_at` (datetime, UTC) | `pol-common-aspects-for-mybizz-anvil-applications` |
| Every core table has `metadata` (Simple Object) | `pol-common-aspects-for-mybizz-anvil-applications`, aspect 4 |
| No column separates clients (`tenant`, `client_id`, `org_id`, `instance_id`) | `adr-dependency-based-not-multi-tenant` |
| No column holds a secret; credentials live only in the Vault | `spec-anvil-platform-standards` |
| The five log and control tables exist: `health_log`, `audit_log`, `error_log`, `webhook_log`, `rate_limits` | test ST-07 |
| Table and column names are the glossary's terms | `GLOSSARY.md` |

## Difference kinds

| Kind | How it is applied | Data |
|---|---|---|
| Addition (table or column) | Through `anvil.yaml` and Resolve | No data affected |
| Rename (table or column) | By David, by hand in the Data Tables view, before `anvil.yaml` is written | Kept |
| Removal (table or column) | Through `anvil.yaml` and Resolve, each checked by name by David | Deleted |
| Type change | As a removal and an addition, each checked by name by David | Deleted |

A rename is taken from `schema-migration-log.md`. When a column disappears and another appears in the same table with no log row, David is asked whether it is a rename.

## Skills and tools

| Skill or tool | Used for |
|---|---|
| `data-models` | Writing the authoritative schema when it is empty; table ownership and client access |
| `anvil-yaml` | Writing and checking `db_schema` in `anvil.yaml` |
| `secure-software-engineering` | Each table's access checked against Step 15's threat model |
| `wizard` | David's instructions: renames, commit, Resolve |
| `anvil --json validate anvil.yaml` | Test ST-01 on `anvil.yaml` |
| `ts_scan.py` | Tests ST-06 and ST-07 on the app |
| `mb-sentinel-review` | Security review, High scrutiny |

## Commands David runs

| When | Where | Command |
|---|---|---|
| After the renames | WSL terminal | `cd /mnt/c/dev/dev-{slug}/{slug}-app{n} && git pull` |
| After the agent writes `anvil.yaml` | WSL terminal | `cd /mnt/c/dev/dev-{slug}/{slug}-app{n} && git pull && gcp` |

## Hand-over to Step 18

| Item | Where |
|---|---|
| App schema, as committed | `{slug}-app{n}\anvil.yaml` |
| Authoritative schema | `docs-standard-local\authoritative-schema.md` |
| Schema migration log | `docs-local\schema-migration-log.md` |
| Step Receipt | `pdlf-outputs\c17\{slug}-c17-{run}-receipt.md` |

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `17` |
| `step_type` | `skill` |
| `skill_family` | `anvil` |
| `run` | From the entry record: `app1`, `app5` or the feature slug |
| `app_number` | From the entry record: 1 or 5 |
| `status` | `complete` when David confirms no schema mismatch remains |
| `synthesized` | `false` |
| `artifact_path` | `{slug}-app{n}\anvil.yaml` |
| `inputs_used` | Step 16 |
