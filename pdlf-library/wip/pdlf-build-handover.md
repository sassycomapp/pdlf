---
title: "pdlf-build-handover"
updated: "2026-10-23"
doc-id: "mb-24ee05ab"
---
# Handover — Building PDLF

## 1. What this is

This handover continues the conversation of 2026-10-21 and 2026-10-22 (titles about the PDLF test suite and the PDLF to-do cleanup) in a fresh context window. Past conversations can be searched; search "PDLF test suite", "pdlf-todo cleanup", "skills pinned", "anvil-cli" for detail behind any point here.

The work is building PDLF: finishing every app-factory step so that PDLF can run an application from conception to release. `mb-3-cs` is the application that will be pulled through PDLF to pressure-test it. The objective is developing PDLF, not developing `mb-3-cs`.

## 2. The working model

- **One AI thinks, one AI builds.** Claude does the architecture and engineering, and writes the documents. OpenCode agents do the building. David approves every change.
- **OpenCode is fenced; Claude is not.** Cupcake (a policy engine) allows or blocks every OpenCode tool call against compiled rules. Claude works without those fences and has no access to David's computer: David runs every command on it.
- **PDLF is a factory, separate from its products.** PDLF holds only management structure. Everything about a project lives in that project's own project library (documents) and its own repositories (code). Nothing of a project is stored in PDLF or in any other register.
- **The ledger is the only register.** PostgreSQL database `pdlf` (Windows PostgreSQL 15, port 5433), seven tables. No dev logs, no other registers.
- **One home for every fact.** A fact lives in one document; every other document links to it.
- **Documentation linking is live.** Documents link to the documents they depend on with `[[name]]` (converted by the `mb-doc-check` commit hook to `[[[source:page]]](path)`). GBrain indexes those links, so a working agent follows them to the underlying source.
- **GBrain is consulted for everything.** Every source of knowledge is in GBrain; every step starts with a GBrain search; the file a search points to is read before it is applied. New knowledge enters GBrain only through the memory governor and `mb-submit-memory`.
- **Only David commits**, with `bash /mnt/c/mybizz/scripts/commit-all.sh "message"`.

## 3. The role of each step document

Every step has a set of seven in its phase folder in `C:\pdlf\app-factory\`, named `{phase letter}{step}-…` (for example `b12-…`):

| Document | Role |
|---|---|
| `-build-plan.md` | Carries the conversion of intent into the application: what the step must achieve, starts from, produces, who carries it out, and what it must be built so that |
| `-reference.md` | Carries the step's structure and its links to every underlying support system and reference the step uses |
| `-explainer.md` | Tells the step as a story, which gives it context and meaning |
| `-decision-tree.html` | The functional map of the step, generated from the reference |
| `-config.md` | The step's fixed values |
| `-test-spec.md` | What the step must prove; a foundation that grows as the step is developed |
| `-module.md` | The skill file the orchestrator executes, pulling the other six into one actionable form; written last |

There is no separate learnings file per step: a lesson goes straight into the document it concerns (build plan rule 4.6).

`C:\pdlf\app-factory\pdlf-build-plan.md` is the at-a-glance summary of the whole process for the orchestrator. There is no single grand map of tools: each step's reference links to the tools and sources that step uses.

## 4. The passes

1. **Pass 1 — get the documentation right.** Every step of every phase (B, C, D, E, F, then A): build plan, config, reference, explainer, decision tree, and the test spec where the build plan changes it. Modules are not written.
2. **Pass 2 — pressure-test the documentation** by pulling `mb-3-cs` through PDLF from beginning to end. What fails or is missing changes PDLF.
3. **Pass 3 — write the modules** from the proven steps. PDLF is then done.

`mb-3-cs` is backed up by David before Pass 2. `mb-5-pdlf` stays as an empty placeholder; it is not used.

## 5. What exists, by category

Read `C:\mybizz\mybizz-os-docs\os-reference-docs\repo-organization.md` for every repository and its path, and `skills-catalog.md` (same folder) for every skill, system and agent. The categories of documents are:

**PDLF** (`C:\pdlf`, repository `pdlf`)
- `app-factory\`: `pdlf-build-plan.md`, `README.md`, and the phase folders `phase-a-init` to `phase-f-ship-and-monitor` with each step's set of seven.
- `pdlf-library\adr-local\` (10 PDLF decisions, for example `no-staging-environment-five-app-isolation`, `global-content-discovery-and-application-discipline`, `skill-use-principle`).
- `pdlf-library\policy-local\` (8: `pol-anvil-platform`, `pol-bft-discipline`, `pol-memory-and-knowledge`, `pol-sequential-enforcement-and-deviation`, `pol-skill-invocation`, `pol-step-conditional-state`, `pol-testing-and-quality`, `pol-INDEX`).
- `pdlf-library\specifications-local\` (7: `spec-artifact-handover`, `spec-bft`, `spec-execution-discipline`, `spec-gate-procedure`, `spec-postgres-ledger`, `spec-skill-context-pack`, `spec-skill-design`).
- `pdlf-library\templates-local\` (BFT cheatsheet, self-test checklist, ISA template, step receipt template, pre-project).
- `pdlf-library\pdlf-explainer-docs\` (`pdlf-explainer`, `app-factory-explainer`, `pdlf-testing-explainer`).
- `pdlf-library\docs-local\` (`pdlf-todo`, `app-factory-docs-update-method`, `config`, `pdlf-skills-scoping-strategy`, `pdlf-built-report`, `judgement-trail`, Matt Pocock skill notes).

**Global standards** (`C:\dev\project-library-global`, repository `project-library-global`, GBrain source `default`): what a good Mybizz application is.
- `adr-global\` (45 decisions), `specifications-global\` (24), `policy-global\` (5), `security-global\` (54: threats, requirements, testing, secrets, cloud), `standard-operating-procedures-global\` (5), `docs-standard-global\` (4), `guides-global\` (2), `templates-global\` (4), `rules-cupcake-global\` (21 Cupcake rules).
- `anvil-docs\` (326 pages): Anvil's own documentation, the canonical Anvil reference.
- `test-suite\`: `ts-method`, `ts-catalogue` (112 tests), `ts-conformance-checks`, `ts-rule-soundness-register`, `tools\` (`ts_scan.py`, `ts_report.py`), `templates\` (`conftest.py`, `ts-config.yaml`, `access-matrix.yaml`, `pytest.ini`).

**Anvil's own agent material**
- `C:\mybizz\anvil-agent-references` (pinned at `14b1967`): Anvil's skills (`anvil-yaml`, `client-forms`, `client-modules`, `data-models`, `server-code`) and their references. With `anvil-docs`, the two principal sources for all application development.
- The Anvil CLI 0.7.7 (pinned): `anvil --json validate <file or folder>` validates app files. Its documents: `mybizz-config-docs\anvil-cli\`. Never used: `anvil watch`, `anvil db apply-schema`, `anvil update`.

**MyBizz OS** (`C:\mybizz\mybizz-os-docs`): `os-reference-docs\` (`repo-organization`, `skills-catalog`, `mybizz-os-explainer`, `memory-master-explainer`, `system-integrity-explainer`, `documentation-linking-explainer`, frontmatter conventions, `mybizz-scope-list`, WSL paths, OpenCode reset) and `operating-procedures\` (commit-all, grant paths, session start, daily ops, standing instruction and others).

**System documents** (`C:\mybizz\mybizz-config-docs`): four documents per system (config, reference, explainer, learnings) for every system MyBizz built or set up its own way (GBrain, Graphify, GStack, Cupcake, memory governor, OpenCode, PostgreSQL, the `mb-` skills, commit-all, `mb-doc-check`, anvil-cli and others), and `mb-config-manager`'s register. Written only by `mb-sysdoc-creator` and `mb-config-manager` (OpenCode), never edited directly.

**Each project library** (`C:\dev\dev-{slug}\{slug}-project-library`): `docs-local`, `adr-local`, `pdlf-outputs\{step}\` (every step's receipt and artefacts), `pdlf-tickets`, `docs-local\schema-migration-log.md`, `docs-local\releases\v{n}\`.

**Code knowledge: Graphify.** GBrain deliberately holds no application code. Graphify builds a knowledge graph of each app's code and answers agent questions from it (it runs as an MCP server). It is the code-knowledge source for every step that reads or changes code (Phases D, E, F), and its graph is rebuilt after code changes. The catalog names it at Steps 11, 12, 16, 34 and 40.

**Skills**, pinned to the versions the steps were designed from (never upgraded without David's decision):

| Skill set | Version | Loaded from |
|---|---|---|
| GStack | 1.91.164.0, commit `c580561`, branch `mybizz-c580561` | `~/.config/opencode/skills/gstack-{name}/` (names unchanged, e.g. `cso`) |
| Matt Pocock | `5beb35b` | `~/.agents/skills/{name}/` |
| Anvil agent references | `14b1967` | `~/.agents/skills/{name}/` |
| Magdoub wireframe | `44a5814` | `~/.config/opencode/skills/wireframe/` |
| Magnus919 security skills | installed files | `~/.config/opencode/skills/` |

Skills not yet built (video documentation and similar) come last and are not needed now.

## 6. How Claude uses GBrain

Claude has no access to David's computer. GBrain is reached through David, in batches:
1. Claude writes its search terms into one file.
2. One read-only script on David's PC runs `gbrain search` for each term and writes all results to one file in `C:\temp`.
3. David attaches that file.

David's addition, to be built first in the next session: a dedicated repository (for example `mb-gbrain-searches`, readable by Claude) that keeps every search script and its results. It becomes a search library: Claude can re-read past results instead of repeating searches, and OpenCode agents can use Claude's searches, which steers their thinking with better queries. Scope it with David before building: repository name, folder layout, file naming, whether it is a GBrain source, and the script itself.

## 7. Phase B: where Pass 1 starts

Method: `C:\pdlf\pdlf-library\docs-local\app-factory-docs-update-method.md`. Per step: close the build plan; check the test spec; write the config, reference and explainer; generate the decision tree; send the files.

| Step | Build plan | Config | Reference | Explainer | Decision tree |
|---|---|---|---|---|---|
| b11 | Closed (the model of a finished build plan) | Written | Written | Written | Written |
| b12 | Open: gathered `## From …` sections | Old | Old | Empty | Old |
| b13 | Placeholder (step not used) | — | — | — | — |
| b14 | Open | Old | Old | Empty | Old |
| b15 | Open (1,200 lines; holds a saved copy of GStack `/plan-eng-review` from 1.58.1, now outdated: remove it and check against `c580561`) | Old | Old | Empty | Old |
| b16 | Open | Old | Old | Empty | Old |

`b11` still needs updating for sections 8 and 9 (it predates the test suite).

## 8. What each Phase B test spec needs from its build plan

| Step | Test spec requires | Missing from the build plan |
|---|---|---|
| b11 | PR-09 (local Anvil App Server, server and client Uplink keys, a `TEST_` user with a second factor, the mail catcher); ST-10 (each app's `.gitignore` covers `.env`; `tests\` holds the four templates); PR-06 | The test setup: copy the templates into each app's `tests\`; `.env` keys `ANVIL_UPLINK_KEY`, `ANVIL_CLIENT_KEY`, `TS_TEST_PASSWORD`; start the App Server |
| b12 | DC-01; DC-02 (sections present; the 14 common aspects stated; no reference platform's technology carried over) | DC-02 |
| b14 | DC-03 (scope; data inventory with protection levels; POPIA, GDPR, PCI SAQ A; exit; Hobby fit) | All of DC-03 as outputs |
| b15 | DC-04 to DC-08 (test plan with catalogue IDs; `access-matrix.yaml`; threat model; security decisions; conformance checks selected) | `access-matrix.yaml`, the security decisions, the conformance selection; its Testing line says "three levels" (the suite has levels D and 0 to 4) |
| b16 | DC-09; PR-05 (receipts match evidence, `ts_report.py --check`); PR-03 | PR-05 |

Each build plan's **Testing** line becomes `{step}-test-spec.md` with one sentence of what it proves.

## 9. Decisions of 2026-10-22 the documents must reflect

- Every client starts on the Anvil **Hobby** plan: background and scheduled tasks; no persistent server; no staging; 1,000 emails a month, 150,000 rows, 10 GB.
- **Release:** App 1's tagged release is pushed into App 2 (`master_template`) by David at Step 42. No `develop`/`stable` branches.
- **Testing:** first on the Anvil App Server on David's PC (empty database each run); only hosted services on hosted App 1 with `TEST_` data; a server Uplink key sets up data, a client key signed in as a role proves access. Target: designed and reviewed against OWASP ASVS 5.0 Level 2 principles, Level 3 on payment, administration and high-value paths.
- **Sign-in:** a second factor for every account holder; the Owner uses FIDO2 only; shoppers buy as guests; remember-me at most 7 days; idle limit 30 minutes; passwords minimum 8, no composition rules.
- **Server functions** return data and raise errors (no envelope). **Money** in whole cents. **Observability:** instances push heartbeats; App 5 never polls.
- **Schema changes** are applied by David in Anvil's Data Tables view (Step 17); no agent runs `anvil db apply-schema`.
- `spec-testing.md` moved to `mb-3-cs-project-library\docs-local\mb-3-cs-test-specification.md`; the `mb-3-cs` Vault details to `mb-3-cs-vault-implementation.md`.
- The ledger's `triage_findings.source_step` also allows 35A, 38A, 40, 41, 42A, 43, 44.

## 10. Corrections to make in PDLF before or during Pass 1

1. **Remove the test-application context** wherever cited (`mb-5-pdlf`, "test application", Daily Intentions Tracker) and make `mb-3-cs` the application Pass 2 pulls through PDLF: `pdlf-build-plan.md` ("First builds", rule 4.8, "What success means"), `app-factory-docs-update-method.md`, `pdlf-testing-explainer.md`, `pdlf-todo.md` (C2, B4), `b12`, `b14`, `b15`, `b16` build plans, `matt-pocock-skills-pdlf-compliance.md`, `matt-pocock-skills-local-reference.md`, `step-receipt-template.md`, `spec-artifact-handover.md`, `spec-postgres-ledger.md`, and `project-library-global\specifications-global\spec-nomenclature.md`.
2. **`pdlf-build-plan.md` section 9:** "Testing: designed as a component of its own" is done; replace with the test suite and the step test specs.
3. **`app-factory-docs-update-method.md`:** its last bullet ("light testing element") is replaced by "Each step's testing is its `{step}-test-spec.md`, drawn from the test suite"; its phase order and passes follow section 4 of this handover.
4. **`pdlf-todo.md`:** remove E1 (resolved on 2026-10-22: skills brought to their pinned versions).
5. **Two testing policies:** `pdlf-library\policy-local\pol-testing-and-quality.md` and `project-library-global\policy-global\pol-testing-and-quality.md` differ. Settle into one home (the global one, rewritten on 2026-10-22 to the test suite) and remove or reduce the local one to PDLF-only content.
6. **A stray copy of PDLF documents** sits in `app-factory\phase-c-design-and-plan\pdlf-library\` (6 files: `pdlf-todo`, `pol-anvil-platform`, `spec-skill-context-pack`, `spec-skill-design`, `app-factory-explainer`, `pdlf-explainer`). Compare with the real ones in `pdlf-library\` and delete the stray folder.
7. **The working model (section 2 and 3 of this handover)** is written as a PDLF document near the orchestrator, so the orchestrator understands what it is dealing with: proposed home `pdlf-library\docs-local\pdlf-operating-model.md`, linked from `pdlf-build-plan.md`.

## 11. Working with David

- Read the memory preferences; they govern every reply. Short, numbered, plain sentences; next action first.
- Scope first. Produce nothing (file, prompt, command) without David's express approval.
- Act as the engineer: decide technical questions; ask David only about intent, each question with a recommended answer and its reason.
- Work from the live repositories (`git clone https://github.com/sassycomapp/{repo}`), never from an old copy: the commit hook rewrites links and dates on every commit.
- Send at most 16 files per send; list each with the exact path it replaces. For many files, a placement script that moves them from Downloads into place has worked well.
- WSL commands one at a time, never in the same reply as an open question.
- OpenCode prompts state plan mode or build mode, and carry every fact the agent needs so it does not search.
- Never place files at `C:\` root; working files go in `C:\pdlf\pdlf-library\wip`, temporary files in `C:\temp`.
- Every open item is closed; nothing is deferred without a home on the to-do list.

## 12. First actions in the next session

1. Scope and build the GBrain search library (section 6) with David.
2. Clone `pdlf` and `project-library-global`; read `pdlf-build-plan.md`, `app-factory-docs-update-method.md`, the `b11` suite and `b11-test-spec.md`.
3. Propose the corrections of section 10 as one batch; on approval, write them.
4. Start Pass 1 with `b11`, then `b12`, `b14`, `b15`, `b16`: for each, the plan first, then the files.
