---
title: "b11-config"
doc-id: "mb-ea7e8074"
updated: "2026-10-29"
---
# Step 11 — Init: Configuration

The fixed values of Step 11. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-b-discover-and-define/b11-reference|Step 11 Reference]]](C:/pdlf/app-factory/phase-b-discover-and-define/b11-reference.md). What the step is and why: [[[pdlf:app-factory/phase-b-discover-and-define/b11-explainer|Step 11 Explainer]]](C:/pdlf/app-factory/phase-b-discover-and-define/b11-explainer.md). What it must prove: [[[pdlf:app-factory/phase-b-discover-and-define/b11-test-spec|Step 11 Test Specification]]](C:/pdlf/app-factory/phase-b-discover-and-define/b11-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 11, Init |
| Phase | B, Discover and Define |
| Carried out by | OpenCode |
| Entry points that run it | 02 (route A), 03 (route B), 07 and 08 (route C) |
| Next step | 12, except entry 07 (App 3), for which Steps 12 to 16 do not run |
| Gate | None |
| BFT level | Full |
| Sentinel scrutiny | High |

## Inputs

| Input | Where |
|---|---|
| Entry record | The `inputs_used` of the run's entry-point row ([[[pdlf:app-factory/phase-a-init/a01-config\|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md)) |
| Business row | The `projects` row: for routes A and B, written by the orchestrator with the slug, the name and the mode |
| Project context (route B) | `C:\dev\dev-{slug}\{slug}-project-context\`, the business's existing documentation, read-only |
| Project template | `C:\dev\project-template\dev-(SLUG)\` |
| Blank pre-project files | `C:\pdlf\pdlf-library\templates-local\pre-project\` |
| Anvil's `AGENTS.md` template and skills | `C:\mybizz\anvil-agent-references\` |
| Test templates | `C:\dev\project-library-global\test-suite\templates\` |
| Local runtime tool | `/mnt/c/dev/project-library-global/test-suite/tools/ts_local.sh` |
| Sign-in settings | [[[default:specifications-global/spec-security\|Security Specification]]](C:/dev/project-library-global/specifications-global/spec-security.md), section 3 |
| The ledger | Database `pdlf`, port 5433, through the PowerShell bridge ([[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger\|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md)) |

## Outputs

| Output | Where |
|---|---|
| Business folder | `C:\dev\dev-{slug}\` |
| App folders | `C:\dev\dev-{slug}\{slug}-app1`, `-app2`, `-app3`, `-app5` |
| App repository | `sassycomapp/{slug}-app{n}` on GitHub, created by David through Anvil |
| Test setup (App 1, App 5) | `{slug}-app{n}\tests\` and `{slug}-app{n}\.env` |
| Project library | `C:\dev\dev-{slug}\{slug}-project-library\`, public GitHub repository `sassycomapp/{slug}-project-library` |
| Project context (route B) | `C:\dev\dev-{slug}\{slug}-project-context\`, GitHub repository `sassycomapp/{slug}-project-context`, GBrain source `{slug}-project-context` |
| Entry receipt (entries 02 and 03) | `{slug}-project-library\pdlf-outputs\a02\` or `a03\`: the entry's checks file and Step Receipt |
| GBrain source | `{slug}-project-library`, federated |
| Ledger | the `projects` row; the Step 11 `steps` row; its BFT record; its `triage_findings` row |
| PR-09 evidence | `{slug}-project-library\pdlf-outputs\b11\{slug}-b11-{run}-pr09.xml` |
| Test results | `{slug}-project-library\pdlf-outputs\b11\{slug}-b11-{run}-checks.xml` (JUnit XML, ts-method section 5); `{slug}-b11-{run}-validate.json`; `{slug}-b11-{run}-gitleaks.json` |
| Step Receipt | `{slug}-project-library\pdlf-outputs\b11\{slug}-b11-{run}-receipt.md` |

## Skills and tools

| Skill or tool | Used for |
|---|---|
| `wizard` | David's exact instructions for creating an app in Anvil and switching on its Users service |
| `setup-matt-pocock-skills` | The Matt Pocock configuration in `docs\agents\` |
| `graphify` | Route B: the code graph of the existing app |
| GStack `/cso` | Route B: the secret scan of the existing public repositories |
| `ts_local.sh` | The local runtime and the PR-09 run |
| `anvil --json validate .` | Test ST-01 on the cloned app |
| `mb-sentinel-review` | Security review, High scrutiny |
| [[[pdlf:pdlf-library/operating-procedures/sop-health-check\|SOP: Health Check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md) | The closing self-audit |

## Foundation checks

| Check | Pass when |
|---|---|
| Ledger | Port 5433 answers; seven tables exist |
| GBrain | It answers; sources `default` and `pdlf` are registered |
| Anvil's skills | `C:\mybizz\anvil-agent-references` exists |
| Anvil command-line tool | `anvil --version` answers |
| Skills | `setup-matt-pocock-skills`, `wizard`, `graphify`, `cso` (GStack), `mb-sentinel-review` and every skill Steps 12 to 16 name are installed |
| Test tools | `java -version` is 21 or later; `gitleaks version` answers; `~/mybizz-test-tools/venv` holds `anvil-app-server`, `anvil-uplink`, `pytest`, `pyotp`, `aiosmtpd` and `PyYAML` at the versions in [[[default:test-suite/ts-method\|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md) section 9 |

## Users service settings

David sets these in the Anvil editor when he creates the app.

| Setting | Value |
|---|---|
| Sign-in | Email and password |
| Require 2-factor authentication | On; authenticator apps and security keys (FIDO2) allowed |
| Require secure passwords | On |
| Email confirmation | Required |
| Remember-me | At most 7 days |
| Allow visitors to sign up | Off |
| Embedding | Off |
| Users table | Text column `role` added in the Data Tables view |

## Test setup

| Item | Value |
|---|---|
| Apps that get it | App 1 and App 5; never App 3 |
| Folders | `tests\logic\`, `tests\integration\`, `tests\security\`, provided by the project template |
| Copied into `tests\` | `conftest.py`, `pytest.ini`, `ts-config.yaml` (with `role: app1`) |
| Copied into `tests\integration\` | `test_pr09_environment.py` |
| David's command for `.env` | `bash /mnt/c/dev/project-library-global/test-suite/tools/ts_local.sh {app folder} init` |
| `.env` keys | `TS_TARGET`, `TS_UPLINK_URL`, `ANVIL_UPLINK_KEY`, `ANVIL_CLIENT_KEY`, `TS_TEST_PASSWORD`, `TS_ROLE_COLUMN` |
| Runtime address | `http://localhost:3030`; mail catcher on port 8025 |

## Fixed answers for the Matt Pocock setup

| Question | Answer |
|---|---|
| Issue tracker | Local markdown files in `pdlf-tickets\` |
| Triage labels | `needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix` |
| Domain documents | Single context, shared by all the business's apps: the glossary `docs-local\GLOSSARY.md`; decisions in `adr-local\`, one file each, `adr-{kebab-case-name}.md`; `docs\agents\domain.md` states both, as the project template holds it |
| `CLAUDE.md` | Never created |

## Bringing an app's repository into its folder

The app folder holds the project template's scaffold, so `git clone` cannot be used. In `{slug}-app{n}`:

```
git init
git remote add origin https://github.com/sassycomapp/{slug}-app{n}.git
git fetch origin
git remote set-head origin -a
git checkout -t "$(git rev-parse --abbrev-ref origin/HEAD)"
```

## The project context (route B)

The commands David runs, one at a time, after renaming the GitHub repository and moving the old library's contents into `{slug}-project-context\`.

| Order | What it does | Command |
|---|---|---|
| 1 | Points the context at its new GitHub address | `git -C /mnt/c/dev/dev-{slug}/{slug}-project-context remote set-url origin https://github.com/sassycomapp/{slug}-project-context.git` |
| 2 | Registers the context in GBrain in place of the old library, after setting a default source that stays | `gbrain sources add {slug}-project-context --path /mnt/c/dev/dev-{slug}/{slug}-project-context && gbrain sources federate {slug}-project-context && gbrain sources default pdlf && gbrain sources remove {slug}-project-library --confirm-destructive` |
| 3 | Puts the context on the commit tools in place of the old library | `sed -i 's#^{slug}-project-library = /mnt/c/dev/dev-{slug}/{slug}-project-library$#{slug}-project-context = /mnt/c/dev/dev-{slug}/{slug}-project-context#' /mnt/c/mybizz/scripts/mb-doc-check.sources && sed -i 's#^  /mnt/c/dev/dev-{slug}/{slug}-project-library$#  /mnt/c/dev/dev-{slug}/{slug}-project-context#' /mnt/c/mybizz/scripts/commit-all.sh` |
| 4 | Points the context's own links at its new name; nothing else in it changes | `cd /mnt/c/dev/dev-{slug}/{slug}-project-context && git ls-files -z '*.md' '*.html' \| xargs -0 sed -i -e 's#\[\[\[{slug}-project-library:#[[[{slug}-project-context:#g' -e 's#C:/dev/dev-{slug}/{slug}-project-library/#C:/dev/dev-{slug}/{slug}-project-context/#g'` |
| 5 | Commits and pushes the context and the scripts, which syncs the context into GBrain | `REPOS_OVERRIDE="/mnt/c/dev/dev-{slug}/{slug}-project-context /mnt/c/mybizz/scripts" bash /mnt/c/mybizz/scripts/commit-all.sh "{slug} library becomes {slug}-project-context"` |

The row of `{slug}-project-context` in `repo-organization.md` names it read-only, with no OpenCode project and no Dream cycle.

## Refreshing the system documents

The OpenCode prompt David runs, in build mode, after the project library or the project context joins GBrain:

> Run `/mb-sysdoc-creator` in Refresh mode for the systems `gbrain` and `mb-doc-check`. The business `{slug}` has new sources. Check each document's list of sources against the output of `gbrain sources list` and against `/mnt/c/mybizz/scripts/mb-doc-check.sources`, and correct only what differs.

## App `.gitignore` baseline

The `.gitignore` in every app folder of the project template. It keeps out `.env`, `.env.*`, credentials, `__pycache__/`, `*.pyc`, `.pytest_cache/`, test output, `.venv/`, `graphify-out/`, `.gbrain/`, `.opencode/`, `.gstack/`.

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `11` |
| `step_type` | `skill` |
| `skill_family` | `opencode` |
| `run` | `app1` for routes A and B; `app3` or `app5` for route C |
| `app_number` | 1 for routes A and B; 3 or 5 for route C |
