---
title: "b11-build-plan"
doc-id: "mb-4f446919"
updated: "2026-10-24"
---
# Step 11 — Init: Build Plan

## Step entry

### Phase B — Discover and Define

Ends with the gate `domain-locked` (Step 16).

#### Step 11: Init

**Must achieve:** a sound foundation for the business and the app being started: its folders and repositories exist and are linked to GitHub, its project library has the standard structure, it is registered in GBrain and covered by the commit tools, its record is in the ledger, and the app is ready to be tested, so that every later step can rely on all of it without checking again.

**Starts from:** the entry record from the orchestrator (build plan section 4); David's answers; the project template at `C:\dev\project-template\dev-(SLUG)\`; the blank pre-project files at `C:\pdlf\pdlf-library\templates-local\pre-project\`; the test suite's templates and `ts_local.sh` at `C:\dev\project-library-global\test-suite\`; the ledger; GBrain.

**Produces:** the business folder `C:\dev\dev-{slug}\` with `README.md`, the app folders `{slug}-app1`, `{slug}-app2`, `{slug}-app3`, `{slug}-app5`, the project library `{slug}-project-library` and `wip`; App 1 (or, for entries 07 and 08, App 3 or App 5) cloned from GitHub into its folder, with the Users service switched on; for an app that holds code (App 1 or App 5), its `tests\` folder with the test templates, its `.env` and a working local runtime; the project library with its standard folders, its `pdlf-outputs\` step folders and `pdlf-tickets\`; for a new application, the three blank pre-project files in `pre-project\`; the Matt Pocock configuration in `docs\agents\`; the GBrain source `{slug}-project-library`; the `projects` row; the PR-09 evidence, the Step Receipt and the BFT record in `pdlf-outputs\b11\`.

**Carried out by:** OpenCode. Four actions belong to David and are never done by the agent: creating each app in Anvil (which creates its code repository on GitHub); switching on the app's Users service and adding its `role` column; writing the app's `.env`; and every commit and push.

**Must be built so that:**
- it reads the entry record and runs one of three routes: **A**, a new business (entry 02); **B**, an application with context (entry 03); **C**, a new app in an existing business (entries 07 and 08);
- before anything is created, it runs the foundation checks: the ledger answers on port 5433 with its seven tables; GBrain answers and the sources `default` and `pdlf` are registered; the clone of Anvil's skills is present at `C:\mybizz\anvil-agent-references`; the Anvil command-line tool `anvil` is installed; every skill this step and Steps 12 to 16 use is installed; the test tools of the test suite are installed at their approved versions (Java 21, `gitleaks`, and in `~/mybizz-test-tools/venv` the Anvil App Server, Anvil Uplink, pytest, pyotp, aiosmtpd and PyYAML); any failure stops the step with a deviation;
- the slug is the business's short name, all lowercase, with its hyphens kept;
- for a new business, the template is copied with `(SLUG)`, `(slug)`, `{slug}` and `{project-name}` replaced, and every `doc-id` line removed from the copied documents, so each project's documents get their own identity at their first commit;
- an app's code repository always comes from Anvil: David creates the app in his Anvil account and connects it to GitHub as `{slug}-app{n}`; the agent gives him exact numbered instructions made with the `wizard` skill, then brings the repository into the app folder, which already holds the project template's scaffold, with `git init`, `git remote add origin`, `git fetch origin` and `git checkout` of the repository's default branch, because `git clone` needs an empty folder; it checks the clone holds `anvil.yaml` and never writes to it;
- the same `wizard` instructions have David switch on the app's Users service with the settings of `spec-security`: email and password sign-in; "Require 2-factor authentication", with authenticator apps and security keys (FIDO2) allowed; "Require secure passwords"; email confirmation required; remember-me at most 7 days; embedding off; new sign-ups off (the access matrix at Step 15 decides them); and add a text column `role` to the Users table in the Data Tables view; the agent then pulls the app and checks `anvil.yaml` holds the Users service;
- every app folder gets an `AGENTS.md` built from Anvil's own template (`C:\mybizz\anvil-agent-references\AGENTS.md`), with its resource paths pointed at that folder, and keeps the `.gitignore` the project template places in it, which keeps out `.env`, credentials, `__pycache__`, test output, the code graph and development files, because everything committed is pushed to Anvil; an app folder without one gets it from the project template; the `.gitignore` is in place before `.env` exists;
- an app that holds code (App 1, App 5) gets its test setup; App 3 holds no code and gets none: the folders `tests\logic\`, `tests\integration\` and `tests\security\`, which the project template provides; the templates `conftest.py`, `pytest.ini` and `ts-config.yaml` copied into `tests\`, with `role: app1` in `ts-config.yaml`; and `test_pr09_environment.py` copied into `tests\integration\`;
- the agent gives David the one command that writes the app's `.env` (`ts_local.sh {app folder} init`), because no agent reads or writes `.env`; the step waits until David confirms;
- the agent starts the local runtime with `ts_local.sh {app folder} start`, runs the PR-09 test through `ts_local.sh {app folder} run`, saves its JUnit output in `pdlf-outputs\b11\`, and stops the runtime; a failure stops the step with a deviation;
- the project library is created on GitHub as a public repository only with David's permission; David's refusal stops the step, because there is no project without it;
- the blank pre-project files are placed in `pre-project\` for a new application, and David is asked to fill them in;
- the Matt Pocock setup runs `setup-matt-pocock-skills` in the project library with PDLF's answers fixed in advance, so David only confirms: tickets are local markdown files in `pdlf-tickets\`; the five standard triage labels; single context, with the glossary at `docs-local\GLOSSARY.md` and decisions in `adr-local\`; the skill never creates a `CLAUDE.md`;
- the project library is registered in GBrain as the federated source `{slug}-project-library`;
- the agent gives David the exact lines that add the project library to `mb-doc-check.sources` and to `commit-all.sh`, and the command that installs the commit hook; the step does not finish until David confirms, because otherwise the project's first commit bypasses the hook;
- for an application with context, nothing that exists is changed: only missing folders and files are created, broken links or registrations are corrected only with David's permission, David confirms each repository's data is sound, and an old name is reported, never renamed; where the app's Users service, its `role` column, its test setup or its `.env` is missing, it is added as in route A, the Users service and `.env` by David;
- for an application with context, a reference platform's material held anywhere in the project library other than `reference-platform-local\` is reported, and moved there only with David's permission, because that folder is ignored by git, so its material is never committed and never indexed by GBrain;
- for an application with context, `graphify` builds the code graph of the existing app, and GStack `/cso` scans the existing public repositories for secrets; a secret found is removed and rotated before the step ends;
- for a new app in an existing business, the health check runs first, then only that app's part is done; the project library is not touched;
- the `projects` row records the slug, the business's name, the mode, the library path, the GBrain source and every app's path and Anvil address known so far;
- the security review `mb-sentinel-review` runs on the step's output at High scrutiny, because the app repositories are public and nothing secret may enter them; a Flag or Escalate stops the step; its `triage_findings` row is checked before the step finishes;
- the step ends with [[[pdlf:pdlf-library/operating-procedures/sop-health-check|SOP: Health Check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md) as its self-audit: every failure is reported, nothing is fixed without David's permission;
- its ledger row is `step_type = 'skill'`, `skill_family = 'opencode'`, `run = 'app{n}'` and `app_number` = `n`, for the app worked on.

**BFT level:** Full, because Step 11 makes the structural decisions everything else stands on.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md), [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md), [[[pdlf:pdlf-library/specifications-local/spec-skill-context-pack|Spec: Skill Context Pack]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-context-pack.md), [[[default:specifications-global/spec-security|Security Specification]]](C:/dev/project-library-global/specifications-global/spec-security.md), [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `setup-matt-pocock-skills` (Matt Pocock): configures Matt's skills for the business, once → every later Matt Pocock skill.
- `wizard` (Matt Pocock): numbered instructions for creating each app in Anvil and switching on its Users service → the clone of each app's repository and test PR-09.
- `graphify`: for an existing application (route B), builds the code graph of the existing app → Steps 12 and 16.
- `/cso` (GStack), static scan: for an existing application (route B), scans the existing public repositories for secrets → this step's Sentinel review.
- `mb-sentinel-review`, High → `triage_findings`, checked before the step finishes.

**Layers with no skill:** display (no design exists yet); GStack workflow (the step only sets up).

**Testing:** [[[pdlf:app-factory/phase-b-discover-and-define/b11-test-spec|Step 11 Test Specification]]](C:/pdlf/app-factory/phase-b-discover-and-define/b11-test-spec.md): the foundation is sound, nothing secret is public, and the app is ready to be tested.

**Standards:** [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md).

## Why it is built this way

- **Three routes, one end.** A new business, an existing one and a new app differ only in how their repositories are obtained and checked. The same closing health check proves each is sound, so every later step can rely on the same foundation.
- **Foundation checks first.** A missing tool found at Step 15 costs a half-finished review; found at Step 11 it costs nothing.
- **Anvil creates the code repository.** An Anvil app's repository must come from Anvil, or Anvil cannot synchronise with it.
- **The app folders hold their scaffold.** The project template gives every app folder its `.gitignore`, `README.md` and, for an app that holds code, its test folders, so every app starts the same. The repository is brought in with `git init` and `git fetch`, because `git clone` works only into an empty folder.
- **David switches on the Users service.** Its settings live in `anvil.yaml`, which no agent writes, and its table is a schema change, which David applies in the Data Tables view. The settings are the same for every Mybizz app, so they are fixed at the start.
- **The test setup at the start.** PR-09 proves the local runtime, both Uplink connections, a `TEST_` user's second factor and the mail catcher once, before any later step relies on them.
- **David writes `.env`.** It holds keys, and no agent reads or writes it; `ts_local.sh` loads it into the processes it starts without showing its values.
- **The template is copied without document identities.** Otherwise every project would share the template's identities, and the commit hook would treat different projects' documents as one.
- **Tickets in the project library.** Tickets are documentation, so they live with the business's documents, never in an app's code.
- **Commit coverage confirmed before the end.** A project library outside the hook would be committed without identities, link repair or a GBrain update.
- **Nothing existing is changed.** An existing application's material is David's.
