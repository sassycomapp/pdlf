---
title: "pdlf-build-plan"
doc-id: "mb-64817b10"
updated: "2026-10-13"
---
# PDLF Build Plan

## Preamble

### Purpose of this document

This is the system build plan for PDLF. It is the single forward-looking document for the PDLF system as a whole: what PDLF is, what it must be, the rules every step is built to, and the decisions that span more than one step. It absorbed the former statement of intent, which is retired. Where any other PDLF document disagrees with this plan, this plan states the intent and the other document is corrected.

This plan is a work in progress. PDLF is in its discovery and conceptualisation stage, and this plan changes whenever a better idea replaces an earlier one. An earlier agreement is never a reason to keep something that a better one has replaced.

This plan holds only what applies to PDLF as a whole. Each step carries its own build plan, as section 7 sets out. Each step's entry, and everything else that belongs to one step, is held in that step's own files.

The work proceeds in three stages. First, PDLF is conceptualised as far as possible and the concept is written into this plan. Second, the steps are scoped one at a time, and this plan is refined as they are. Third, once every step is scoped and the design is known to produce the kind of application wanted, the steps are built.

### 1. What PDLF is, and whom it serves

PDLF, the Project Development Lifecycle Framework, is an application development system. It builds Anvil.works applications.

PDLF is a system, not a project. It has no code repository of its own. It lives at `C:\pdlf` (WSL path `/mnt/c/pdlf`), in the private GitHub repository `sassycomapp/pdlf`, and its documents form the GBrain source `pdlf`, which covers the whole of `C:\pdlf`. All work on PDLF happens there. There is no workshop and no second copy.

PDLF runs on mybizz-os, the operating system that supplies its memory, governance, documentation tools and close-out. The two are parts of one package: mybizz-os keeps the environment sound, and PDLF uses that environment to build applications.

Three names are never confused. **Mybizz** is the company. **mybizz-os** is the operating system. **PDLF** is the system that builds Mybizz's applications. Each application PDLF builds is its own Mybizz business.

PDLF is built and run by a team of three:

| Member | Role |
|---|---|
| David | Project manager and developer. Decides intent, approves every change, and alone commits. |
| Claude (Anthropic, web interface) | Architect and engineer. Designs PDLF and resolves its technical questions. |
| OpenCode and its models | The worker. Carries out the steps. |

David is a project manager acting as developer. He reads code but is not a programmer, so he depends on PDLF and its agents to make the code correct. PDLF therefore carries the responsibility for correct code, and it explains every decision to David in plain language, so that he stays in control without having to judge code himself.

The credo for PDLF, and for everything in it, is: **simple, secure, robust, fit for purpose.** Nothing is kept for ceremony, and nothing is kept for posterity.

**What a project is.** A project is one Mybizz business that PDLF develops. Each project lives in its own folder at `C:\dev\dev-{slug}\`, where the slug is the business's short name (for example `mb-3-cs`, `mb-4-ecom`, `mb-5-pdlf`). Every project folder holds the same scaffold:

```
C:\dev\dev-{slug}\
  README.md
  {slug}-app1              code repository of App 1, the development workspace
  {slug}-app2              code repository of App 2, master_template
  {slug}-app3              code repository of App 3, blank_client_template
  {slug}-app5              code repository of App 5, the management tooling
  {slug}-project-library   the project library: the working documentation for the whole business
  wip                      David's temporary working folder; not part of the project
```

Each code repository is one Anvil application and synchronises with Anvil through GitHub. The project library holds everything else for all of the business's apps: documents, decisions and PDLF records. Code and documentation are never mixed. One project library serves the whole business because its apps share one design, one vocabulary and one set of decisions; anything specific to one app has its own folder inside the library. The project library is the project's GBrain source.

No project data is stored in PDLF; all project data is stored in the project folders at `C:\dev\`.

**Step outputs.** Every project library holds a folder `pdlf-outputs\`, with one folder per step, named as in the app factory: `a01\` to `a10\`, `b11\` to `b16\`, `c17\` to `c28\`, `d29\` to `d34\`, `e35\` to `e40b\` and `f41\` to `f46\`, including `b13\` and `c25\`. Everything a step produces for that project is kept in its folder, whichever skill produced it: the step's receipt, a copy of every artifact a skill saved elsewhere (GStack, for example, saves in its own place), and the artifacts of skills that are told where to save (such as Archify, the Magdoub wireframe skills and Sentinel), which save there directly. Each file name begins with the slug, the step and the run (`app` for the whole application, or the feature's short name), for example `mb-5-pdlf-b15-app-test-plan.md`, so the step and the run that produced it are clear and a feature never overwrites the application's files. Step 11 creates the folders for a new project.

The business slug is the business's short name as recorded at Step 11, all lowercase, with its hyphens kept. Each app's folder and repository is named `{slug}-app{n}`, with no descriptive word. App 4 lives on the client's own Anvil account and has no folder. Application code is never a GBrain source: agents read it directly from the app folder.

### 2. Control and gates

PDLF never runs on its own. The orchestrator is David's tool for building an application, not an autonomous agent.

Every change PDLF makes needs David's approval, until David says that a particular approval is no longer needed. More interaction is preferred to less. Interaction can be reduced later, as confidence in PDLF grows, but only by David, never by PDLF itself.

The gates are essential. A gate is a hard stop at which David approves a commitment before anything is built on it. PDLF never passes a gate without that approval, and never oversteps or jumps one. Cupcake, the policy engine of mybizz-os, enforces this. That Cupcake actually does so while PDLF runs must be proven by a deliberate test, not assumed.

PDLF runs under the same rules as all OpenCode work: the global `AGENTS.md` and Cupcake. It has no separate rule system of its own. Its access to each application's folders is set when the orchestrator is designed.

When a step cannot be done as written, the agent stops, sets out the options and what each one costs, and David decides. The decision is recorded in the ledger. Nothing is skipped without a recorded decision.

Why: an AI agent left to itself drifts, skips steps and decides things nobody asked it to decide. David cannot catch that by reading code. Control therefore has to be built into how PDLF runs, not left to the agent's good behaviour.

### 3. The five-app structure

PDLF builds many Anvil applications, each a separate business of Mybizz. Every business has its own dedicated set of five apps, as set out in [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md):

| App | Name | What it is |
|---|---|---|
| App 1 | `{dev-workspace}` | The development workspace. All feature work happens here. It is never a dependency of any client instance. |
| App 2 | `master_template` | The published dependency. The sole source of all server-side logic and UI forms for every client instance. |
| App 3 | `blank_client_template` | The provisioning clone source. The sole source from which new client instances are cloned. |
| App 4 | `[client-name]-{vertical}` | One per paying client: a dedicated, isolated app instance. |
| App 5 | `{Product}_management` | The platform operator's internal tooling: provisioning, health monitoring, billing automation and update distribution. |

**Which apps PDLF develops.** PDLF develops Apps 1, 3 and 5. App 2 and App 4 are produced from them, never developed directly.

**App 2 is always a clone of App 1.** It has nothing of its own. It exists so that work in progress on App 1 never reaches clients. Only when David is satisfied with work in App 1 is it released, by cloning App 1's approved code into App 2, as a gated step David approves. That release is a system-wide update, and it reaches every client at once, because every client instance depends on App 2. There is no separate staging or production environment. App 1's documents, in the project library, cover App 2.

**App 4 is a clone of App 3.** Every client has its own Anvil account. David owns every one of these accounts, but each account bears the name of the client's business: for a client whose business is `marysyoga.com`, App 3 is cloned into the `marysyoga.com` account, and that instance is the client's App 4. The only thing unique to a client instance is that client's own data, in its own database and data tables, so App 4 has nothing to document and no folder in the project. PDLF builds and verifies one instance, the provisioning procedure, and the README every instance must carry. That first instance is the first real client, also used as the test client. Provisioning each later client follows the procedure as normal business operations, outside the pipeline.

**Hosting.** Apps 1, 2, 3 and 5 are hosted on David's Anvil account, each at a numbered subdomain of the business's domain: for MB-3-CS, `1.mb3cs.site`, `2.mb3cs.site`, `3.mb3cs.site` and `5.mb3cs.site`. App 4 is hosted on the client's own Anvil account.

**GBrain.** Every project library, like every other documentation repository, is a GBrain source, and all of them can be searched together. When an application re-enters PDLF, PDLF reads its repositories directly.

**No application is ever multi-tenant.** This is permanent and sealed by [[[default:adr-global/adr-dependency-based-not-multi-tenant|ADR: Dependency-Based, Not Multi-Tenant]]](C:/dev/project-library-global/adr-global/adr-dependency-based-not-multi-tenant.md). Every client has its own application instance and its own database. No application ever shares one database between clients and separates them by filtering. This rule has no exceptions. AI agents are given it as context before any code is generated, because they reach for shared-database patterns by default.

**Design.** Every application uses Anvil's Material 3 theme and David's design standards in `project-library-global`. Design moves in approved stages: structural wireframes, then polished wireframes, then screens. David approves each stage before the next begins.

**Quality.** Every feature is built, tested and signed off by David before the next feature begins. Each feature is tested at three levels: its logic on its own, then connected to the live Anvil application, then by hand in the browser. The findings of every review and every quality check are written to a file; a review that left no file did not happen. How PDLF tests is designed as a component of its own (section 9).

**First builds.** A small test application, the Daily Intentions Tracker, goes through PDLF first, in `mb-5-pdlf`, so that PDLF's own faults are found cheaply, before they can damage a real business. It can be extended if it proves too small to test PDLF fully. `mb-3-cs` (Mybizz CS, consulting and services) follows, then the other Mybizz businesses, such as `mb-4-ecom` (e-commerce).

### 4. Entry points

PDLF is one continuous pipeline. Not all work starts at its beginning: work on an app that already exists does not re-scope what the app is about. The entry point decides where the work joins the pipeline and which steps run.

David starts PDLF by running `/pdlf-init` in OpenCode. This starts Step 1, the orchestrator, whose first job is to offer the entry points. Steps 2 to 10 are the entry points. Their numbers imply no order, and exactly one is chosen:

| Step | Entry point | App worked on | Where the work joins the pipeline |
|---|---|---|---|
| 02 | `new-app-no-context` | App 1 | Step 11, at the project slug question. |
| 03 | `new-app-with-context` | App 1 | Step 11, at the repository questions. The application may be partly developed but has not yet run through PDLF; the orchestrator establishes what context material exists. |
| 04 | `add-feature-main-app` | App 1 | Health check, then the feature path (below). |
| 05 | `update-main-app` | App 1 | Health check, then the update path (below). |
| 06 | `compile-master-template` | App 2 | A step near the end of the pipeline, not Phase B. |
| 07 | `create-client-template` | App 3 | Step 11, at the project slug question or the repository questions, depending on whether there is existing context or not. Steps 12 to 16 do not run for App 3. |
| 08 | `create-management-app` | App 5 | Step 11, at the project slug question or the repository questions, depending on whether there is existing context or not. |
| 09 | `add-feature-management-app` | App 3 or App 5 | Health check, then the feature path (below). |
| 10 | `update-management-app` | App 3 or App 5 | Health check, then the update path (below). |

For every entry point except 02 and 03, the orchestrator asks David questions to establish which application is meant, and for 04, 05, 09 and 10 also where the work begins.

**Why Steps 12 to 16 do not run for App 3.** App 3 holds only App 1's data table schema, one startup module and its dependency on App 2. There is nothing in it to design.

**The entry record.** Before Step 11 or Step 12 runs, the orchestrator establishes the entry record: the entry point chosen; the business slug and the app worked on (1, 3 or 5); the path (a whole application, a feature or an update); for a feature or an update, a short statement of it in David's words and a short name for it (the feature slug), which the orchestrator asks David for; and the project's mode, `full` or `test`. For entries 04 to 10 the orchestrator writes the entry record at once to the ledger row of the step where the entry joins. For entries 02 and 03 no business row exists yet, so the orchestrator passes the entry record to Step 11, which writes the business row first and then the entry record. The mode is kept in the business row, because it belongs to the business, not to one entry. Every step reads the entry record from the ledger and never asks David again for what it already says.

**Health check.** Every entry point that works on an app that already exists (04 to 10) first runs the health check, the standard procedure [[[pdlf:pdlf-library/operating-procedures/sop-health-check|SOP: Health Check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md). Step 11 runs the same procedure as its closing self-audit. No work starts until every check passes. Step 11 is not repeated.

**The feature path.** A new feature is scoped, but the application is not re-scoped. The work starts at Step 12, which describes the feature and checks it against the application's existing design, then runs through the reviews and domain modelling of Steps 14 to 16 at the size of the feature.

**The update path.** The orchestrator asks David whether the update changes what the application does. If it does, it is a feature and takes the feature path. If it only corrects or adjusts what already exists, the work goes to the step David nominates.

**A new application.** A new application with no prior context (02) starts from three pre-project files: a brief, scoping ideas, and constraints and notes. The blank set of these files is part of PDLF and ships with it, because more than one step reads it; it is kept current with the pipeline. An application with context (03) brings its own instead.

**Where the pipeline ends.** The pipeline ends when the application, feature or update has been built, tested and deployed into the five-app structure, and commissioned into service. The steps that build the remaining apps are added after the current Step 46, in `phase-g`. The current Step 46 is a learning step and moves to the end of the whole pipeline.

Why: an update or a feature on an app that is already defined does not need the app defined again, but it does need its own scoping and a sound setup to build on.

### 5. How PDLF runs

PDLF runs inside OpenCode, through the OpenCode Build agent and its model.

**The orchestrator** is Step 1. It offers the entry points, runs the steps selected for the chosen entry point in order, and stops at every gate. Its design is completed in parts, alongside the steps it runs, and is finished only when every step is designed.

**Steps and modules.** Every step lives in `app-factory/`, in the folder of its phase: `phase-a-init` (1 to 10), `phase-b-discover-and-define` (11 to 16), `phase-c-design-and-plan` (17 to 28), `phase-d-scaffold-and-assemble` (29 to 34), `phase-e-build-and-verify` (35 to 40b) and `phase-f-ship-and-monitor` (41 to 46); `phase-g` is added for the remaining apps when they are designed. Step numbers are global and never renumbered within a phase, because the number is the step's identity in the ledger, the gates, the receipts and every document. Steps 13 and 25 are not used. Inserted steps carry a lowercase letter after the number, only to keep the files in order: 35a, 38a, 40b and 42a. Every step has the same six files, the set of six (section 7), named with the phase letter and the step number, for example `b11-module.md`. Steps 13 and 25 each keep one placeholder file instead. When a step is built, it is compiled into its module: a single, self-contained unit holding the finished step and everything only that step needs. Until then the module is empty. Anything several modules need about how PDLF itself works lives once, in `pdlf-library`.

**What goes to Anvil.** Everything committed to a code repository is pushed to Anvil and stored there, so `.gitignore` keeps out everything that must stay local, such as `.env`, credentials and test output. Anvil uses only `anvil.yaml`, `client_code`, `server_code` and `theme`. Two parts are public: every file in `theme/assets` can be opened by anyone with its link, and the code in `client_code` runs in the user's browser, where it can be read. Nothing secret, internal or for paying clients only ever goes in either. Client-facing documents, such as user guides, may be served from `theme/assets/docs`. Explainer videos are hosted on YouTube and linked or embedded. No agent ever writes `anvil.yaml`; Anvil manages it. The code repository is pulled to local after every step in which work was done in the Anvil editor.

**Instruction files.** `AGENTS.md` is PDLF's single instruction file; there is no `CLAUDE.md`. A PDLF `opencode.json` is written when the orchestrator is designed, because only then is it known what PDLF needs beyond the global settings.

**Artifacts.** Every artifact is written to its canonical place. Where that place is outside the project's step folder, a copy is also written to the step folder (section 1), so that each step's outputs for a project are all in one place.

### 6. Knowledge, skills, learning and records

**Knowledge.** Each kind of knowledge has exactly one home, and a fact lives in only one of them:

- `pdlf-library` (in `C:\pdlf`) holds how PDLF itself works.
- `project-library-global` (`C:\dev\project-library-global`) holds what a good application is: Anvil knowledge, standards, specifications and decisions that apply to every application. It is project-agnostic and permanent, and it is the standard every application is built to.
- An application's own documentation repository (its `docs-local`) holds what is true of that one application only.

The one deliberate exception is nomenclature. All names are defined in a single document, [[[default:specifications-global/spec-nomenclature|Spec: Nomenclature]]](C:/dev/project-library-global/specifications-global/spec-nomenclature.md): one part for what is common, one for PDLF, and one for each application. A term is defined once.

**Anvil compliance is the central tenet.** All development is fully compliant with Anvil.works: Anvil's standards, specifications, principles and methods are applied throughout every application. The two principal sources of reference for all application development are `C:\mybizz\anvil-agent-references` (the skills issued directly by Anvil, which are how agents apply Anvil correctly) and `C:\dev\project-library-global\anvil-docs` (a compilation of Anvil's own documentation, without its images). They are the principal sources, not the only ones. Where two Anvil sources conflict, the conflict is raised to David, who resolves it; neither source silently wins. Standards and instructions form one consistent whole: a conflict between them is a defect, fixed at its source.

**GBrain is consulted at all times.** Every source of knowledge is submitted to GBrain, indexed and embedded, so that GBrain is fully informed, and one GBrain search covers all of it. Every step starts with a GBrain search, GBrain is consulted whenever knowledge is needed, and the actual file a search points to is read before it is applied. New knowledge enters GBrain only through the memory governor and `mb-submit-memory`. PDLF may propose changes to `project-library-global` when a lesson concerns Anvil or application standards, and David approves them.

**Skills.** PDLF consists only of the skills that best serve its objectives: nothing superfluous and nothing lacking. Its skills come from GStack, Matt Pocock, Magdoub's wireframe skills and Anvil's `anvil-agent-references`. The curated set is listed in `C:\mybizz\mybizz-os-docs\os-reference-docs\skills-catalog.md`, the single register of skills; most of them are installed on the computer. A skill joins PDLF only if it earns its place; once there, it is always used for its task, and the agent never improvises a task a skill covers. When each step is designed, the catalog is considered as a whole and the skills that best serve the step are deployed in it. This is critical: a step designed without considering the catalog misses what the installed skills already do well.

**Learning and self-healing.** PDLF must never learn the same lesson twice or repeat a mistake. Each lesson is written once, into the source that will actually be read next time: a lesson about Anvil or about good applications goes into `project-library-global`; a lesson about how PDLF works goes into the step, rule or specification concerned; a lesson about one application goes into that application's own documentation. When a step fails, or David corrects something, PDLF proposes the fix to that source and David approves it. Every lesson is committed to GBrain through the memory governor and `mb-submit-memory`. How each step learns is part of that step's design. Why: a lesson kept in a log is a lesson nobody reads.

**The ledger.** PDLF keeps one database record of every build: database `pdlf` on the Windows PostgreSQL 15 server, port 5433. It holds seven tables: projects, steps, gates, deviations, BFT records, ISC records and triage findings. The ledger is control, not ceremony: it lets the orchestrator refuse to pass a gate that was never approved, and lets a build resume or re-enter where it left off. Its connection details live in `.env`, which never leaves the computer. Detail: [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md). An application built by PDLF needs no judgement trail of its own: the ledger records every gate and deviation, and every step explains itself in plain language.

**Close-out and commits.** Close-out is the mybizz-os skill `/mb-close-out`, run when David asks for it. Only David commits and pushes, using `commit-all`; agents never do.

**What PDLF refuses.** Ceremony: reports and logs nobody reads, duplicate records, steps that exist only to look careful (stops and checks are not ceremony; they are how David controls the build). Unearned skills. Silent decisions. Shared databases.

**What success means.** PDLF succeeds when it is perpetually learning and self-healing, so that the development lifecycle is stable and dependable; when Anvil's standards are applied throughout every application it builds; and when it consists only of the skills that best serve its objectives. These claims are earned by real builds, starting with the test application, not by design alone.

### 7. The documents and their life cycle

Every PDLF document has one job, and a fact lives in only one of them.

- **This system build plan** holds what applies to PDLF as a whole. It is forward-looking.
- **The set of six.** Every step has six files in its phase folder, named with the phase letter and step number (here Step 11): `b11-build-plan.md`, `b11-config.md`, `b11-reference.md`, `b11-explainer.md`, `b11-decision-tree.html` and `b11-module.md`. They exist for every step from the start, empty until the step is worked on.
- **Each step's build plan** (`b11-build-plan.md`) holds that step's design while it is being worked out. Every step's entry, and all other material that belongs to that step, is held there, so that each step carries everything it needs when it is designed.
- **When a step is built,** its build plan is turned into three documents, the same pattern as the rest of mybizz-os: `b11-config.md` (agent-facing: the step's fixed values, such as its inputs, outputs, file paths, skills, gate and BFT level); `b11-reference.md` (agent-facing: what the agent does, in order); and `b11-explainer.md` (for the agent and for David: what the step is, how it works and why). Its decision tree (`b11-decision-tree.html`) stays beside them, as the picture of the reference, and is kept matching it. The step's module is compiled from these files. The step's build plan then moves to `obsolete/`. A fact lives in only one of the three documents.
- **The step documents are functional, not historical.** They describe the step as it is, never how it came to be.
- **The built report** (`pdlf-library/docs-local/pdlf-built-report.md`) is the historical account of PDLF's own development, and only of PDLF, never of the applications PDLF builds. Entries are only ever added, never edited. Any history worth keeping goes there.
- **When the last step is built,** this plan is retired to `obsolete/`. Its system-wide content moves into small, single-subject documents in `pdlf-library/docs-local/`.
- **The older step material** (the existing step files, build notes and the `stepwise` folder) stays in place as source material. It is drawn on when each step is designed, and is not changed before then.

Why: each step is complex enough to need its own plan, and one plan for every step would grow too large to work with. A plan that dissolves into the step's own documents as the step is built leaves nothing behind to drift.

### 8. Rules every step follows

Every step is built to these rules. They are stated once here and not repeated in each step. Every step follows [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md), applies [[[pdlf:pdlf-library/specifications-local/spec-bft|Spec: BFT]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md), and names things per [[[default:specifications-global/spec-nomenclature|Spec: Nomenclature]]](C:/dev/project-library-global/specifications-global/spec-nomenclature.md). References that apply to particular steps are named at those steps.

- **It starts with a GBrain search** of the federated documentation sources (one search covers the project library `{slug}-project-library`, `default`, which is `project-library-global`, and `pdlf`). A step that needs Anvil knowledge also names `anvil-agent-references-code`. Application code is never searched in GBrain; it is read directly from the app folder. The step reads the actual file a search points to before applying it.
- **The developer approves every change.** The step explains each decision in plain language, never jumps a gate, and never passes one without the developer's approval.
- **Skills take precedence.** When a skill in PDLF's library covers a task, the step uses it and does not improvise.
- **Deviations are decided by the developer.** If the step cannot be done as written, it stops, sets out the options and what each costs, and the developer decides. The decision is recorded in the ledger.
- **It leaves its record:** a row in the ledger, its BFT record at its level, and a Step Receipt at `{slug}-project-library\pdlf-outputs\{step}\{slug}-{step}-{run}-receipt.md`.
- **Every artifact goes to its canonical place,** with a copy in the step's output folder, `{slug}-project-library\pdlf-outputs\{step}\`, when its canonical place is elsewhere.
- **The agent never commits or pushes.** Close-out is `/mb-close-out`, run when the developer asks for it; new knowledge and every lesson reach GBrain only through the memory governor and `mb-submit-memory`.
- **No application is ever multi-tenant.** Every step that shapes data or code keeps each client's application and database separate.

### 9. What is still to be settled

- **Steps work:** the orchestrator's form and its `opencode.json`; where entry point 06 joins the pipeline; which gates exist, where they sit and what each approves; the place and weight of the BFT thinking checkpoints; which `project-library-global` standard each step applies; whether applications receive a `CLAUDE.md`; the steps that build the remaining apps in `phase-g`; and the design of every step, one at a time, with Steps 42 to 44 rebuilt around the release by cloning App 1 into App 2. The step entries in each step's build plan were written before the four-repository scaffold and the clone release; each is corrected to them when its step is designed, Step 11 first. The detailed list is kept in [[[pdlf:pdlf-library/docs-local/pdlf-todo|Active PDLF To-Do List]]](C:/pdlf/pdlf-library/docs-local/pdlf-todo.md).
- **The Cupcake proof:** once the orchestrator exists, an agent deliberately attempts to pass a gate without approval, and Cupcake must block it.
- **Testing:** designed as a component of its own, starting from a review of the testing disciplines.

### 10. How each step is designed

**4.1 Intent first, then the plan, then the step.** For each step, write its build-plan entry first (what it must achieve, what it starts from, what it produces, who carries it out, what it must be built so that), and have the developer approve the entry before the step file is touched. The step file is then written to the entry, never the other way round.

**4.2 Choose skills from the catalogue, deliberately.** For each step, read the catalogue and name the skill that best serves it, with the reason. Read that skill's own source before designing around it, and record what it really does in the build-plan entry. Phase C has clear candidates that were not used in Phase B: Anvil's `data-models`, `anvil-yaml` and `client-forms` for the tables and forms; `wizard`, which walks a person through steps only they can perform, for the manual steps in the Anvil editor (Steps 17, 29 and 32); and `writing-for-agents` whenever a step file is written, because step files are instructions for an agent.

**4.3 Anvil and our standards in every step.** Every build-plan entry names the `project-library-global` standard and the Anvil skill it applies. This is the table "which standard each step applies", built step by step instead of afterwards.

**4.4 One home for every rule.** Rules that apply to every step live once in the build plan. A step file holds only what is particular to that step. No step repeats a shared rule in its own words.

**4.5 One step file, nothing beside it.** No new build notes and no hand-drawn decision trees. If a picture is needed, it is generated from the step file, so that it cannot drift.

**4.6 A lesson goes straight into its source.** When building a step teaches something, the lesson is written at once into the build plan's rules, the specification it concerns, or `project-library-global`, never only into a log.

**4.7 Fit for purpose before thoroughness.** For each step, ask whether it earns its place. Phase C has three near-identical "pull to local" steps (18, 30 and 33): one shared procedure may serve all three. For each review, ask what only it covers, so that the developer is never asked the same question twice.

**4.8 Proven before finished.** A step is recorded as built when its step file is complete, and as finished only after it has run on the test application and been packaged as its module. Phase C is run on the test application as soon as its steps are written, not after the whole pipeline exists.

---

## The Build Plan

### The steps

Every step's entry is held in its own build plan, `{letter}{number}-build-plan.md`, in its phase folder (section 7). Steps 13 and 25 are not used; each has a placeholder file.

### Phase G — Remaining apps

**Must achieve:** the steps that build the rest of the five-app set in the same pipeline: `blank_client_template`, the first client instance with the provisioning procedure and the README every instance carries, and the management tooling. Not yet designed.
