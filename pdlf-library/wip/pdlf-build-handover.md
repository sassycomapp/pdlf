---
title: "pdlf-build-handover"
updated: "2026-10-29"
doc-id: "mb-24ee05ab"
---
# Handover — Building PDLF

## 1. What this is

This handover continues the conversations of 2026-10-21 to 2026-10-29 in a fresh context window. Past conversations can be searched; search "PDLF test suite", "pdlf-todo cleanup", "skills pinned", "anvil-cli", "sanity sweep", "apple tree", "mb-5-pdlf removal", "three-tier testing", "Phase B Pass 1", "GLOSSARY.md", "project template scaffold", "phase by phase" for detail behind any point here.

The work is building PDLF: finishing every app-factory step so that PDLF can run an application from conception to release. `mb-3-cs` is the application that will be pulled through PDLF to pressure-test it. The objective is developing PDLF, not developing `mb-3-cs`.

The sanity sweep of PDLF, `project-library-global`, `mybizz-os-docs`, `data-mybizz-mgt`, `dev-root-hub` and `mybizz-config-docs` is complete and committed (section 12). The working model below is stated in full in `pdlf-build-plan.md` (Preamble and sections 5 to 7); this section is its summary. Phase B is built. PDLF is completed phase by phase (section 4): Phase A is built next, for Phases A and B, and then `mb-3-cs` runs through both (section 7).

## 2. The working model

- **One AI thinks, one AI builds.** Claude does the architecture and engineering, and writes the documents. OpenCode agents do the building. David approves every change.
- **OpenCode is fenced; Claude is not.** Cupcake (a policy engine) allows or blocks every OpenCode tool call against compiled rules. Claude works without those fences and has no access to David's computer: David runs every command on it.
- **The dependency rule (the apple tree).** `project-library-global` is the universal context library for every Anvil app and depends on nothing, ever. PDLF is the machine; `mybizz-os-docs` is its support system. Global structures may name a project where they support it, but never depend on an application's files: no application file is a source of truth for them, they link into no application for facts, and they hold no application-only content. Each project, and PDLF, holds only material canonical to itself.
- **PDLF is a factory, separate from its products.** Everything about a project lives in that project's own project library (documents) and its own repositories (code). Nothing of a project is stored in PDLF or in any other register.
- **The ledger is the only register.** PostgreSQL database `pdlf` (Windows PostgreSQL 15, port 5433), seven tables. No dev logs, no judgement trail, no other registers.
- **Documents state only what is.** No history, no posterity, no "previously" or "moved from". A short cautionary note in an explainer ("method B fails for X") is allowed. A document that is only history is deleted. `pdlf-built-report.md` tracks PDLF build work only and is deleted when PDLF is finished.
- **One home for every fact.** A fact lives in one document; every other document links to it.
- **Documentation linking is live.** Documents link to the documents they depend on with `[[name]]` (converted by the `mb-doc-check` commit hook to `[[[source:page]]](path)`). The hook repairs links by doc-id after a rename or move, and stops a commit when a deleted document is still linked. GBrain indexes the links, so a working agent follows them to the underlying source.
- **GBrain is consulted for everything.** Every documentation source is in GBrain; application code is not (Graphify covers code). Every step starts with a GBrain search; the file a search points to is read before it is applied. New knowledge enters GBrain only through the memory governor and `mb-submit-memory`.
- **Only David commits.** Every commit names only the repositories it needs, so David's uncommitted work elsewhere (he works in `mb-4-ecom` in parallel) is never picked up:
  `REPOS_OVERRIDE="/mnt/c/pdlf" bash /mnt/c/mybizz/scripts/commit-all.sh "message"`
  Add `SKIP_SYNC=1` to skip the GBrain sync when several commits follow each other; run one sync with the last commit.

## 3. The role of each step document

Every step has a set of seven in its phase folder in `C:\pdlf\app-factory\`, named `{phase letter}{step}-…` (for example `b12-…`):

| Document | Role |
|---|---|
| `-build-plan.md` | Carries the conversion of intent into the application: what the step must achieve, starts from, produces, who carries it out, and what it must be built so that |
| `-reference.md` | The step's actions in order, each linked to the system or source it uses |
| `-explainer.md` | Tells the step as a story, which gives it context and meaning |
| `-decision-tree.html` | The functional map of the step, generated from the reference |
| `-config.md` | The step's fixed values, including its BFT level |
| `-test-spec.md` | What the step must prove, drawn from the test suite; grows as the step is developed |
| `-module.md` | The skill file the orchestrator executes, pulling the other six into one actionable form; written once its step is proven |

There is no separate learnings file per step: a lesson goes straight into the document it concerns (build plan rule 4.6).

`C:\pdlf\app-factory\pdlf-build-plan.md` is the at-a-glance summary of the whole process for the orchestrator. It is deleted when the last step is built. There is no single grand map of tools: each step's reference links to the tools and sources that step uses.

## 4. The order of work

PDLF is completed phase by phase. Every phase is **built** (its suites written), then **proven** (`mb-3-cs` runs through it and PDLF is corrected), then **finished** (its modules written).

1. Phase B is built.
2. Phase A is built for Phases A and B: every entry point, the orchestrator as far as it runs Phases A and B, and the resume check (the orchestrator reads the ledger and offers to continue an unfinished run where it stopped).
3. Phases A and B are proven, then finished: `mb-3-cs` runs through them by entry point 03, made by Step 11 in a copy of the project template, with its existing repositories as context.
4. Phases C, D, E and F follow, one at a time: each is built, the orchestrator is extended to run it, the `mb-3-cs` run resumes where it stopped (never from the start), and the phase is proven, then finished.

David backs up `mb-3-cs` before every run. The method, the order of work, its steps and its list of banned terms: `C:\pdlf\pdlf-library\docs-local\app-factory-docs-update-method.md`. Every file is scanned against the banned terms before it is sent. The banned wording "three levels of testing" bans only the words: the method is Levels 1, 2 and 3 of the test suite (section 11).

## 5. What exists, by category

Read `C:\mybizz\mybizz-os-docs\os-reference-docs\repo-organization.md` for every repository and its path, and `skills-catalog.md` (same folder) for every skill, system and agent. `C:\dev\dev-root\docmap.md` maps every folder.

**PDLF** (`C:\pdlf`, repository `pdlf`)
- `app-factory\`: `pdlf-build-plan.md`, `README.md`, and the phase folders `phase-a-init` to `phase-f-ship-and-monitor` with each step's set of seven.
- `pdlf-library\adr-local\` (5): `artifact-saving-convention`, `global-content-discovery-and-application-discipline`, `no-staging-environment-five-app-isolation`, `postgres-ledger`, `skill-use-principle`.
- `pdlf-library\policy-local\` (8): `pol-anvil-platform`, `pol-bft-discipline`, `pol-memory-and-knowledge`, `pol-sequential-enforcement-and-deviation`, `pol-skill-invocation`, `pol-step-conditional-state`, `pol-testing-and-quality` (PDLF-only: the per-feature build loop of Steps 35 to 39 and the `build-verified` gate), `pol-INDEX`.
- `pdlf-library\specifications-local\` (7): `spec-artifact-handover`, `spec-bft`, `spec-execution-discipline`, `spec-gate-procedure` (holds the seven gates), `spec-pdlf-process-tests` (PR-01 to PR-10), `spec-postgres-ledger`, `spec-skill-context-pack`.
- `pdlf-library\templates-local\`: `chk-pdlf-self-test`, `isa-template`, `step-receipt-template`, `pre-project\`.
- `pdlf-library\pdlf-explainer-docs\`: `pdlf-explainer`, `app-factory-explainer`, `pdlf-testing-explainer`.
- `pdlf-library\docs-local\`: `pdlf-todo`, `app-factory-docs-update-method`, `config`, `pdlf-skills-scoping-strategy`, `pdlf-built-report`, `matt-pocock-skills-local-reference`.
- `pdlf-library\wip\`: this handover; `pdlf-overview-v4` (the planned steps, phase by phase, for judging gaps and surplus); `pdlf-pass2-demand-map` (what `mb-3-cs` and `mb-4-ecom` demand of each step's skills, for the skills scoping strategy). Each is deleted when its work is done.

**Global standards** (`C:\dev\project-library-global`, repository `project-library-global`, GBrain source `default`): what a good Mybizz application is.
- `adr-global\` (40), `specifications-global\` (24), `policy-global\` (5), `security-global\` (53), `standard-operating-procedures-global\` (3), `docs-standard-global\` (4), `guides-global\` (2), `templates-global\` (4), `rules-cupcake-global\` (21 Cupcake rules).
- `anvil-docs\` (326 pages): Anvil's own documentation, the canonical Anvil reference.
- `test-suite\`: `ts-method`, `ts-catalogue` (102 application tests), `ts-conformance-checks`, `ts-rule-soundness-register`, `tools\` (`ts_scan.py`, `ts_report.py`), `templates\` (`conftest.py`, `ts-config.yaml`, `access-matrix.yaml`, `pytest.ini`).
- Tier prices (Launch, Pioneer, Business) are common to every application and live in `adr-tiers-model`.

**Anvil's own agent material**
- `C:\mybizz\anvil-agent-references` (pinned at `14b1967`): Anvil's skills (`anvil-yaml`, `client-forms`, `client-modules`, `data-models`, `server-code`) and their references. With `anvil-docs`, the two principal sources for all application development.
- The Anvil CLI 0.7.7 (pinned): `anvil --json validate <file or folder>` validates app files. Its documents: `mybizz-config-docs\anvil-cli\`. Never used: `anvil watch`, `anvil db apply-schema`, `anvil update`.
- An HTTP endpoint `@anvil.server.http_endpoint("/path")` is served at `[base_url]/_/api/path`; the canonical webhook pattern is in `adr-webhook-architecture`.

**MyBizz OS** (`C:\mybizz\mybizz-os-docs`): `os-reference-docs\`, `operating-procedures\` and `os-decisions\` (decisions about MyBizz's own tooling: dev-tooling repositories on GitHub, the embedding provider, tooling credentials, build-artefact timestamps).

**System documents** (`C:\mybizz\mybizz-config-docs`): four documents per system (config, reference, explainer, learnings). Written only by its own skills, `mb-sysdoc-creator` and `mb-config-manager`, through OpenCode.

**The project template** (`C:\dev\project-template`, repository `project-template`): the full scaffold of a Mybizz business, from which Step 11 makes every project. Every folder has a `README.md` stating what belongs in it. It is not a GBrain source and is not in `commit-all.sh`: David commits it by hand with plain `git`. It holds:
- the app folders, each with its `.gitignore` and `README.md`; App 1 and App 5 also with `tests\logic\`, `tests\integration\`, `tests\security\`, `scripts\` and `theme\assets\docs\`;
- the project library: `pre-project`, `docs-local` (with `design\`, `strategy\`, `releases\`, `GLOSSARY.md`, `schema-migration-log.md`), `docs-standard-local` (22 standard documents), `adr-local`, `policy-local`, `specifications-local`, `standard-operating-procedures-local`, `guides-local`, `legal-local` (the clause builder's default clauses, Mybizz's agreements with the client, the compliance record and the PAIA manual App 5 publishes), `prompts-local`, `templates-local`, `assets-local`, `ui` (one folder per package, every one kept; the model form folder `(PACKAGE-NAME)\(FORM-NAME)\`), `wireframe`, `docs\agents`, `pdlf-tickets`, `pdlf-outputs\{step}\`, `reports-local` (skill reports outside PDLF), `reference-platform-local` (a reference platform's source, reference and notes, ignored by git and therefore never indexed by GBrain), `.out-of-scope`, `V2`, `wip`.

**Each project library** (`C:\dev\dev-{slug}\{slug}-project-library`) has the template's folders. Application terms go in the project's `GLOSSARY.md`.

**Projects:** `mb-3-cs` and `mb-4-ecom` (`C:\dev\dev-mb-3-cs`, `C:\dev\dev-mb-4-ecom`), each with `{slug}-app1`, `-app2`, `-app3`, `-app5` and `{slug}-project-library`. Fixing either project is outside the PDLF work. Notes for `mb-3-cs` from the sweep are in `C:\dev\dev-mb-3-cs\wip\` (`mb-3-cs-notes-from-global-sweep.md`, `mb-3-cs-nomenclature-part3.md`), for when `mb-3-cs` is worked on.

**Code knowledge: Graphify.** Graphify builds a knowledge graph of each app's code and answers agent questions from it (an MCP server). It is the code-knowledge source for every step that reads or changes code (Phases D, E, F); its graph is rebuilt after code changes.

**Skills**, pinned to the versions the steps were designed from (never upgraded without David's decision):

| Skill set | Version | Loaded from |
|---|---|---|
| GStack | 1.91.164.0, commit `c580561`, branch `mybizz-c580561` | `~/.config/opencode/skills/gstack-{name}/` (names unchanged, e.g. `cso`); native saves under `~/.gstack/projects/{slug}/` |
| Matt Pocock | `5beb35b` | `~/.agents/skills/{name}/` |
| Anvil agent references | `14b1967` | `~/.agents/skills/{name}/` |
| Magdoub wireframe | `44a5814` | `~/.config/opencode/skills/wireframe/` |
| Magnus919 security skills | installed files | `~/.config/opencode/skills/` |

Skills not yet built (video documentation and similar) come last and are not needed now.

## 6. How Claude uses GBrain

Claude has no access to David's computer. GBrain is reached through the search library, the public repository `mb-gbrain-searches` at `C:\mybizz\mb-gbrain-searches` (`/mnt/c/mybizz/mb-gbrain-searches`). Its `README.md` carries the full rules.

1. Claude gives David one command that writes `queries/{yyyy-mm-dd}-{topic}.md` (one search term per line) and runs the script:
   `cd /mnt/c/mybizz/mb-gbrain-searches && printf '%s\n' "term one" "term two" > queries/{name}.md && bash scripts/run-search.sh {name}`
2. The script runs `gbrain search "{term}" --source-id __all__ --limit 10 --snippet-chars 800 --json` for each term, across every source, writes `results/{name}.md`, then commits and pushes that repository only.
3. Claude reads `results/{name}.md` from GitHub. Each result shows `source:page`, its score and up to 800 characters of its text. A result is a pointer: the file it names is read before anything in it is applied.

Rules:
- Claude reads past results in `results/` before running a new search, and never repeats a search it already holds.
- The script only reads GBrain. GBrain 0.59.18.0 stays until David decides otherwise.
- The script never overwrites a results file; a re-run takes a new name.
- The repository is not a GBrain source, has no `mb-doc-check` hook and is not in `commit-all.sh`.

## 7. What comes next

### Phase A, then the first run

To-do A2 sets the job: build Steps 1 to 10 (every entry point; the orchestrator as far as it runs Phases A and B; the resume check), and in the same batch amend Step 11's route B so that an application with context is made in a copy of the project template, with its existing repositories as context, settling how its existing app repositories are carried into the copy. The Phase A suites are old drafts. Then David backs up `mb-3-cs` and it runs through Phases A and B by entry point 03.

### Phase B, the model

Phase B is built: b11, b12, b14, b15 and b16 are closed, and their suites are the model of a finished step. b13 is a placeholder (step not used). Phase B ends at the gate `domain-locked` (Step 16), which locks the glossary, its decisions, the data design and every other Phase B output (section 9).

### Phase C, the next phase to be built

Phase C is built once Phases A and B are proven: Steps 17 to 28, in order. Per step: close the build plan; correct the test spec; write the config, reference and explainer afresh from the closed plan; generate the decision tree; scan every file; update the built report; send the files.

| Step | Build plan | Config | Reference | Explainer | Decision tree |
|---|---|---|---|---|---|
| c17 | Open: carried-over block | Old | Old | Empty | Old |
| c18 | Open | Old | Old | Empty | Old |
| c19 | Open | Old | Old | Empty | Old |
| c20 | Open | Old | Old | Empty | Old |
| c21 | Open | Old | Old | Empty | Old |
| c22 | Open | Old | Old | Empty | Old |
| c23 | Open | Old | Old | Empty | Old |
| c24, c25 | Placeholders (steps not used) | — | — | — | — |
| c26 | Open | Old | Old | Empty | Old |
| c27 | Open | Old | Old | Empty | Old |
| c28 | Open | Old | Old | Empty | Old |

The build plans of `a01` and `e35`, and the reference of `e35`, still say "three levels" of testing and test Level 2 against the live app; they are rewritten to the test suite's Levels 1 to 3 and the local runtime (section 11) when closed. The open build plans f42, f42A, f43 and f44 still model a staging and production split and `develop`/`stable` branches; they are rebuilt around the release by push (section 10) when closed. Old Phase C to F documents name `docs-local\design-doc.md` and older output folders; they read the run's design folder (section 10) when rewritten.

Findings for later steps, settled when each is built:
- **c17:** builds the tables from the data design locked at `domain-locked`, named in the glossary's terms, every table `client: none`, checked against the access matrix and the threat model; the agent writes `db_schema` only through `anvil-yaml`, and David applies it in the Data Tables view.
- **c19:** `to-tickets` reads the glossary and the decisions through `docs\agents\domain.md`; each ticket names its acceptance and security tests by the test plan's catalogue IDs.
- **c23:** GStack's review pipeline runs CEO, design, developer experience, then engineering last, so the engineering review sees the final plan; PDLF runs the engineering review at Step 15 because Step 17 builds the tables from it. Any change `/plan-design-review` makes to the reviewed plan's architecture goes back through `/plan-eng-review`. `/plan-devex-review` does not apply: Mybizz applications are built for end users, not developers.
- **c26, d31:** forms designed after Step 15 are added to the app's `access-matrix.yaml`.
- **e38:** GStack's test plan is saved under the project library's GStack name; `/qa-only`, started from an app repository, has another GStack name and does not find it, so the step pastes `test-plan.md` and GStack's test plan into it.

Old configs and references in every phase still link to `makepdlf`/`stepwise` documents that do not exist, or name the retired `two-gate-extension` ADR in plain words; each is rewritten afresh when its step is built.

## 8. How every step is built

These requirements apply to every step built, without exception.

1. **Do the job; do not discuss it.** First a task list of the supporting structures the step needs, then a task list per document; then the work; then the files. No rounds of findings and questions.
2. **Ask David only what Claude is truly incapable of deciding.** Claude is the engineer and David is not a programmer. A technical choice is Claude's; only an intent that cannot be found in any document is David's, asked with a recommended answer and its reason.
3. **Excellence, not shortcuts.** Autonomy is not licence to do less. Every step is engineered fully and checked before it is sent.
4. **The skills catalogue is the mainstay.** For every step, read `skills-catalog.md` as a whole and draw the skills that best serve the step, never only those its old documents name. Each skill suite's own pipeline (GStack: think, plan, build, review, test, ship, reflect; Matt Pocock: grill, spec, tickets, implement, review) is part of its design and spans several PDLF steps and phases: follow it, and record any step where PDLF departs from it, with the reason. A skill the catalogue gives to a step, or a step a skill's pipeline needs, is written into the catalogue's PDLF steps column in the same batch.
5. **Read the sources first.** The step's old documents, every document it links to, the steps before and after it, the ledger, Sentinel's table, the skills catalogue, and the pinned source of every skill it uses (GStack `c580561`, Matt Pocock `5beb35b`). Design around what a skill really does, including what Cupcake blocks (sub-agents; every domain off the allowlist).
6. **The order of work.** Close the build plan; correct the test spec; write the config, reference and explainer afresh; generate the decision tree; scan; send.
7. **The decision tree.** Generated from the reference. Every action box carries the number of its reference item, and every step's numbering starts from 1. Its diagram code is validated before it is sent.
8. **Supporting structures are fixed at their source,** in the same batch, whenever a step needs them: a shared rule, a template, a tool, a name.
9. **The scan.** Every file: no dead link, no banned term, no wording about what came before, no dependency on an application's files, every named path real.
10. **The built report, every step.** Keeping `pdlf-built-report.md` current is a requirement of every step: its entry is brought to its status, its files and links to its explainer and configuration, in the same batch as the step.
11. **Delivery.** Each file with the path it replaces or a note that it is new, and the one `REPOS_OVERRIDE` commit command for every repository touched.

## 9. What Phase B hands to Phase C

| Item | Where (in `{slug}-project-library\`) | Written at | First read at |
|---|---|---|---|
| Design doc, the reviewed plan with the data design | `docs-local\design\{run}\design-doc.md` | 12, 14, 15, 16 | 17 |
| First concept | `docs-local\design\{run}\design-doc-first-concept.md` | 12 | 21 |
| Test plan | `docs-local\design\{run}\test-plan.md` | 15 | 19 |
| Access matrix | `docs-local\design\app{n}\access-matrix.yaml` | 15 | 17 |
| Threat model | `docs-local\design\app{n}\threat-model.md` | 15 | 17 |
| Glossary | `docs-local\GLOSSARY.md` | 16 | 17 |
| Decisions | `adr-local\adr-{kebab-case-name}.md` | 14, 15, 16 | 17 |
| Reference-platform research | `docs-local\reference-platform-research.md` | 12 | 15, 20 |
| Diagrams and domain map | `pdlf-outputs\b15\`, `pdlf-outputs\b16\` | 15, 16 | 17, 34 |
| Receipts and test results | `pdlf-outputs\b11\` to `b16\` | 11 to 16 | 17 (PR-01) |

Every test result a step records without its own JUnit output goes into `{slug}-{step}-{run}-checks.xml`, and every receipt carries the table `ts_report.py --prefix {slug}-{step}-{run}-` prints (`ts-method` section 5). Phase C steps follow the same rule.

## 10. Decisions the documents must reflect

- Every client starts on the Anvil **Hobby** plan: background and scheduled tasks; no persistent server; no staging; 1,000 emails a month, 150,000 rows, 10 GB.
- **Release:** App 1's tagged release is pushed into App 2 (`master_template`) by David at Step 42. No `develop`/`stable` branches.
- **Apps and names:** `{slug}-app1`, `-app2`, `-app3`, `-app5`; role names `master_template`, `blank_client_template`, `[client-name]-{vertical}`, `{Product}_management` (`spec-nomenclature`).
- **Testing:** first on the Anvil App Server on David's PC (empty database each run); only hosted services on hosted App 1 with `TEST_` data; a server Uplink key sets up data, a client key signed in as a role proves access. Target: OWASP ASVS 5.0 Level 2 principles, Level 3 on payment, administration and high-value paths. Findings files for Steps 36, 37 and 38 are `{slug}-{step}-{run}-findings.md`.
- **Sign-in:** a second factor for every account holder; the Owner uses FIDO2 only; shoppers buy as guests; remember-me at most 7 days; idle limit 30 minutes; passwords minimum 8, no composition rules.
- **Server functions** return data and raise errors (no envelope). **Money** in whole cents. **Observability:** instances push heartbeats; App 5 never polls.
- **Schema changes** are applied by David in Anvil's Data Tables view (Step 17); no agent runs `anvil db apply-schema`. `anvil.yaml` changes only through Anvil's `anvil-yaml` skill.
- **Runs:** `{run}` is `app{n}` for a whole application (`app1`, `app2`, `app3`, `app5`) or the feature slug; a feature slug is unique in the business and never `app{n}`. The ledger's `steps.run` has no default.
- **Glossary:** `docs-local\GLOSSARY.md`, the name the pinned Matt Pocock skills use, single context, shared by all the business's apps; ADRs are `adr-local\adr-{kebab-case-name}.md`; `docs\agents\domain.md` in the project template states both.
- **Design docs:** each run's concept lives in `docs-local\design\{run}\` (`design-doc.md`, `design-doc-first-concept.md`); a reference platform's research in `docs-local\reference-platform-research.md`. From Step 14 on, `design-doc.md` is the reviewed plan: GStack's plan reviews amend it in place and keep `## GSTACK REVIEW REPORT` as its last section. Later steps read these paths.
- **Protection levels:** Public, Internal, Personal, Restricted (`spec-security-architecture` section 4).
- **No `TODOS.md`:** a deferral is written in the plan's NOT in scope section with its reason.
- **Per app and per run:** `access-matrix.yaml` and `threat-model.md` belong to the app, in `docs-local\design\app{n}\`, and a feature extends them; `test-plan.md` belongs to the run, in `docs-local\design\{run}\`. The threat model holds no open weakness, because the project library is public; an open weakness is a ledger finding.
- **Artefacts:** named `{slug}-{step}-{run}-{name}`; GStack project name `sassycomapp-{slug}-app{n}` (`artifact-saving-convention`).
- The `mb-3-cs` context is `C:\dev\dev-mb-3-cs\mb-3-cs-project-context`, read-only: GBrain source `mb-3-cs-project-context`, never opened in OpenCode, because its `AGENTS.md`, `CLAUDE.md` and `opencode.json` are prior material, not instructions. Step 11 makes the new `mb-3-cs-project-library` from the project template. The `mb-3-cs` test specification is `mb-3-cs-project-context\docs-local\mb-3-cs-test-specification.md`; its Vault details are in `mb-3-cs-vault-implementation.md`.
- The ledger's `triage_findings.source_step` also allows 35A, 38A, 40, 41, 42A, 43, 44.

## 11. Testing: the three tiers

The three-tier method (pure logic, Uplink integration, verification in the browser) is Levels 1, 2 and 3 of the test suite. It is mandatory and runs in strict order; no level is skipped (`ts-method` rule 10).

| Tier | Test-suite level | Catalogue tests | Where it runs |
|---|---|---|---|
| Pure logic | Level 1, Logic | LG | Local Python (pytest) |
| Uplink integration | Level 2, Integration | IN | The local Anvil App Server; hosted App 1 only for hosted services |
| Verification in the browser | Level 3, Browser | BR (BR-09 is David's sign-off) | Hosted App 1 |

- The suite adds Level D (documents), Level 0 (static checks) and Level 4 (release) around the three tiers.
- **Backups:** App 1 is backed up before and after every run on hosted App 1. Level 3 always runs on hosted App 1, so every feature gets both backups. Local runs need none.
- **Role checks:** each role's navigation is proven by the browser test BR-03; David accepts each feature at BR-09.
- **Where the tiers apply:** they need built code, so they run from Step 35 on: Steps 35, 35A, 36, 38, 39, 41 and 46. Steps before 35 use Level D and Level 0.
- **Policies:** the testing rules are in `project-library-global\policy-global\pol-testing-and-quality.md`. PDLF's `policy-local\pol-testing-and-quality.md` holds only the order of Steps 35 to 39 and links to the global one.

## 12. State after the sanity sweep

- Committed and pushed: `pdlf`, `project-library-global`, `mybizz-os-docs`, `data-mybizz-mgt`, `dev-root-hub`, `mybizz-config-docs`, `mybizz-scripts`, `mb-project-docs`, `mb-close-out`. Full copies of the first five before the sweep are in `C:\backup-pre-pdlf-sanity-sweep` (with a copy of `/etc/fstab`).
- `mb-5-pdlf` no longer exists: removed from Anvil, GitHub, David's PC, GBrain, OpenCode, fstab, `commit-all.sh`, `mb-doc-check.sources`, the skills and every document. It is a banned term.
- The judgement trail is retired; its rules have homes.
- `docmap.md` matches the real folders; it is rebuilt with `python3 /mnt/c/mybizz/scripts/build-docmap.py --write`.
- `pdlf-todo.md`: E1 (verify the security skills and GBrain results against the steps) is done for each phase before it is proven; E5 (help and video documentation) is done before Phase E is built.
- The stray copy of PDLF documents under `phase-c-design-and-plan\pdlf-library\` is gone. `pdlf-build-plan.md` names the test suite and the step test specifications.
- `project-template` holds the full scaffold (section 5); Steps 11 and 12 and the health check match it.
- Two links do not match their target's exact name and the hook lists them as older broken links (not blocking): in `pdlf-explainer`, the link to `pol-INDEX` is written `pol-index`; in `pdlf-skills-scoping-strategy`, the link to `data-mybizz-mgt` folder `Tools and apps` is written `tools-and-apps`. Fix both in the Phase A batch.

## 13. Working with David

- Read the memory preferences; they govern every reply. Short, numbered, plain sentences; next action first; one fixed step list that never grows.
- Scope first. Produce nothing (file, prompt, command) without David's express approval; ask before sending any file.
- Act as the engineer: decide technical questions; ask David only about intent, each question with a recommended answer and its reason.
- Work from the live repositories (`git clone https://github.com/sassycomapp/{repo}`), never from an old copy: the commit hook rewrites links and dates on every commit.
- Send at most 16 files per send; list each with the exact path it replaces. For many files, send one patch per repository (`git diff --cached --binary`), applied with `git -C {repo} apply --check` then `git apply`.
- Before handing over any deletion or rename, scan every repository for links to the deleted or renamed document; a remaining link blocks the commit.
- On David's PC, the commit hook rewrites links during a blocked commit, so a follow-up fix matches the text by content, not by a patch.
- WSL commands one at a time, never in the same reply as an open question.
- OpenCode prompts state plan mode or build mode, and carry every fact the agent needs so it does not search. Ignore OpenCode's own suggested commit command; give David the `REPOS_OVERRIDE` form.
- Never place files at `C:\` root; working files go in `C:\pdlf\pdlf-library\wip`, temporary files in `C:\temp`.
- Every open item is closed; nothing is deferred without a home in `pdlf-todo.md`.

## 14. First actions in the next session

1. Clone `pdlf`, `project-library-global` and `project-template`; read `pdlf-build-plan.md`, `C:\pdlf\pdlf-library\docs-local\app-factory-docs-update-method.md`, the Phase B suites (`b11` to `b16`, the models of a finished step), section 9, and the Phase A suites (`a01` to `a10`).
2. Build Phase A as to-do A2 and section 7 set out, built as section 8 sets out.
3. Then David backs up `mb-3-cs`, and `mb-3-cs` runs through Phases A and B.
