---
title: "pdlf-build-plan"
doc-id: "mb-f735d552"
updated: "2026-10-12"
---
# PDLF Build Plan

## Preamble

### Purpose of this document

This is the system build plan for PDLF. It is the single forward-looking document for the PDLF system as a whole: what PDLF is, what it must be, the rules every step is built to, and the decisions that span more than one step. It absorbed the former statement of intent, which is retired. Where any other PDLF document disagrees with this plan, this plan states the intent and the other document is corrected.

This plan is a work in progress. PDLF is in its discovery and conceptualisation stage, and this plan changes whenever a better idea replaces an earlier one. An earlier agreement is never a reason to keep something that a better one has replaced.

This plan holds only what applies to PDLF as a whole. Each step carries its own build plan, as section 7 sets out. The step entries below the preamble are kept here until each step's own plan takes them over.

The work proceeds in three stages. First, PDLF is conceptualised as far as possible and the concept is written into this plan. Second, the steps are scoped one at a time, and this plan is refined as they are. Third, once every step is scoped and the design is known to produce the kind of application wanted, the steps are built.

### 1. What PDLF is, and whom it serves

PDLF, the Project Development Lifecycle Framework, is an application development system. It builds Anvil.works applications.

PDLF is a system, not a project. It has no code repository of its own. It lives at `C:\pdlf` (WSL path `/mnt/c/pdlf`), in the private GitHub repository `sassycomapp/pdlf`, and its documents form the GBrain source `pdlf`, which covers the whole of `C:\pdlf`. All work on PDLF happens there. There is no workshop and no second copy.

PDLF runs on mybizz-os, the operating system that supplies its memory, governance, documentation tools and close-out. The two are parts of one package: mybizz-os keeps the environment sound, and PDLF uses that environment to build applications.

Three names are never confused. **Mybizz** is the company. **mybizz-os** is the operating system. **PDLF** is the system that builds Mybizz's applications. Each application PDLF builds is its own Mybizz business.

PDLF serves David, the developer, and his collaborators: Claude and the OpenCode agent. David is a project manager acting as developer. He reads code but is not a programmer, so he depends on PDLF and its agents to make the code correct. PDLF therefore carries the responsibility for correct code, and it explains every decision to David in plain language, so that he stays in control without having to judge code himself.

The credo for PDLF, and for everything in it, is: **simple, secure, robust, fit for purpose.** Nothing is kept for ceremony, and nothing is kept for posterity.

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

**App 2 is a release of App 1.** It has nothing of its own. It exists so that work in progress on App 1 never reaches clients. Only when David is satisfied with work in App 1 is it released to App 2, through the `develop` → `stable` merge, which David performs as a gated step. That release is a system-wide update, and it reaches every client at once, because every client instance depends on App 2. There is no separate staging or production environment.

**App 4 is a clone of App 3.** The only thing unique to a client instance is that client's own data in its own database. PDLF builds and verifies one instance, the provisioning procedure, and the README every instance must carry. That first instance is the first real client, also used as the test client. Provisioning each later client follows the procedure as normal business operations, outside the pipeline.

**Repositories.** Apps 1, 3 and 5 each have their own code repository, which is the Anvil app itself, and their own documentation repository, which holds everything else: documents, decisions and PDLF records. The two are never mixed. App 2 and App 4 have no documentation repository: App 1's documents cover App 2, and App 4 has nothing to document. Every documentation repository is a GBrain source, and all of them can be searched together, because the apps depend on each other. When an application re-enters PDLF, PDLF reads its repositories directly.

**No application is ever multi-tenant.** This is permanent and sealed by [[[default:adr-global/adr-dependency-based-not-multi-tenant|ADR: Dependency-Based, Not Multi-Tenant]]](C:/dev/project-library-global/adr-global/adr-dependency-based-not-multi-tenant.md). Every client has its own application instance and its own database. No application ever shares one database between clients and separates them by filtering. This rule has no exceptions. AI agents are given it as context before any code is generated, because they reach for shared-database patterns by default.

**Design.** Every application uses Anvil's Material 3 theme and David's design standards in `project-library-global`. Design moves in approved stages: structural wireframes, then polished wireframes, then screens. David approves each stage before the next begins.

**Quality.** Every feature is built, tested and signed off by David before the next feature begins. Each feature is tested at three levels: its logic on its own, then connected to the live Anvil application, then by hand in the browser. The findings of every review and every quality check are written to a file; a review that left no file did not happen. How PDLF tests is designed as a component of its own (section 9).

**First builds.** A small test application, the Daily Intentions Tracker, goes through PDLF first, in `mb5pdlf`, so that PDLF's own faults are found cheaply, before they can damage a real business. It can be extended if it proves too small to test PDLF fully. `mb-3-cs` (Mybizz CS, consulting and services) follows, then the other Mybizz businesses, such as `mb4ecom` (e-commerce).

### 4. Entry points

PDLF is one continuous pipeline. Not all work starts at its beginning: work on an app that already exists does not re-scope what the app is about. The entry point decides where the work joins the pipeline and which steps run.

David starts PDLF by running `/pdlf-init` in OpenCode. This starts Step 1, the orchestrator, whose first job is to offer the entry points. Steps 2 to 10 are the entry points. Their numbers imply no order, and exactly one is chosen:

| Step | Entry point | App worked on | Where the work joins the pipeline |
|---|---|---|---|
| 02 | `new-app-no-context` | App 1 | Step 11, at the project slug question. |
| 03 | `new-app-with-context` | App 1 | Step 11, at the four repository questions. The application may be partly developed but has not yet run through PDLF; the orchestrator establishes what context material exists. |
| 04 | `add-feature-main-app` | App 1 | The feature path (below). |
| 05 | `update-main-app` | App 1 | The update path (below). |
| 06 | `compile-master-template` | App 2 | A step near the end of the pipeline. To be settled. |
| 07 | `create-client-template` | App 3 | Probably Step 11. To be settled. |
| 08 | `create-management-app` | App 5 | Probably Step 11. To be settled. |
| 09 | `add-feature-management-app` | App 3 or App 5 | The feature path (below). |
| 10 | `update-management-app` | App 3 or App 5 | The update path (below). |

For every entry point except 02 and 03, the orchestrator asks David questions to establish which application is meant, and for 04, 05, 09 and 10 also where the work begins.

**Health check.** Every entry point that works on an app that already exists (04 to 10) first checks the app's setup: its repositories exist and are linked, it is registered in GBrain, and it has its record in the ledger. No work starts on a broken setup. Step 11 is not repeated.

**The feature path.** A new feature is scoped, but the application is not re-scoped. The work starts at Step 12, which describes the feature and checks it against the application's existing design, then runs through the reviews and domain modelling of Steps 14 to 16 at the size of the feature.

**The update path.** The orchestrator asks David whether the update changes what the application does. If it does, it is a feature and takes the feature path. If it only corrects or adjusts what already exists, the work goes to the step David nominates.

**A new application.** A new application with no prior context (02) starts from three pre-project files: a brief, scoping ideas, and constraints and notes. The blank set of these files is part of PDLF and ships with it, because more than one step reads it; it is kept current with the pipeline. An application with context (03) brings its own instead.

**Where the pipeline ends.** The steps that build the remaining apps are added after the current Step 46, in `phase-g`. The current Step 46 is a learning step and moves to the end of the whole pipeline.

Why: an update or a feature on an app that is already defined does not need the app defined again, but it does need its own scoping and a sound setup to build on.

### 5. How PDLF runs

PDLF runs inside OpenCode, through the OpenCode Build agent and its model.

**The orchestrator** is Step 1. It offers the entry points, runs the steps selected for the chosen entry point in order, and stops at every gate. Its design is completed in parts, alongside the steps it runs, and is finished only when every step is designed.

**Steps and modules.** Every step lives in `app-factory/`, in the folder of its phase: `phase-a-init` (1 to 10), `phase-b-discover-and-define` (11 to 16), `phase-c-design-and-plan` (17 to 28), `phase-d-scaffold-and-assemble` (29 to 34), `phase-e-build-and-verify` (35 to 40b) and `phase-f-ship-and-monitor` (41 to 46); `phase-g` is added for the remaining apps when they are designed. Step numbers are global and never renumbered within a phase, because the number is the step's identity in the ledger, the gates, the receipts and every document. Steps 13 and 25 are not used. Inserted steps carry a lowercase letter: 35a, 38a, 40b and 42a. When a step is built, it is compiled into its module file, `NN-module.md`, in the same folder: a single, self-contained unit holding the finished step and everything only that step needs. Until then the module file is a placeholder. Anything several modules need about how PDLF itself works lives once, in `pdlf-library`.

**What goes to Anvil.** Everything committed to a code repository is pushed to Anvil and stored there, so `.gitignore` keeps out everything that must stay local, such as `.env`, credentials and test output. Anvil uses only `anvil.yaml`, `client_code`, `server_code` and `theme`. Two parts are public: every file in `theme/assets` can be opened by anyone with its link, and the code in `client_code` runs in the user's browser, where it can be read. Nothing secret, internal or for paying clients only ever goes in either. Client-facing documents, such as user guides, may be served from `theme/assets/docs`. Explainer videos are hosted on YouTube and linked or embedded. No agent ever writes `anvil.yaml`; Anvil manages it. The code repository is pulled to local after every step in which work was done in the Anvil editor.

**Instruction files.** `AGENTS.md` is PDLF's single instruction file; there is no `CLAUDE.md`. A PDLF `opencode.json` is written when the orchestrator is designed, because only then is it known what PDLF needs beyond the global settings.

**Artifacts.** Every artifact is written to its canonical place, and a copy is also written to `output/` for David's convenience. `output/` serves one application at a time; each copy is copied into the application's own folders, its arrival is verified, and only then is it cleared from `output/`.

### 6. Knowledge, skills, learning and records

**Knowledge.** Each kind of knowledge has exactly one home, and a fact lives in only one of them:

- `pdlf-library` (in `C:\pdlf`) holds how PDLF itself works.
- `project-library-global` (`C:\dev\project-library-global`) holds what a good application is: Anvil knowledge, standards, specifications and decisions that apply to every application. It is project-agnostic and permanent, and it is the standard every application is built to.
- An application's own documentation repository (its `docs-local`) holds what is true of that one application only.

The one deliberate exception is nomenclature. All names are defined in a single document, [[[default:specifications-global/spec-nomenclature|Spec: Nomenclature]]](C:/dev/project-library-global/specifications-global/spec-nomenclature.md): one part for what is common, one for PDLF, and one for each application. A term is defined once.

Anvil's standards, specifications, principles and methods are applied throughout every application. There are two sources of Anvil knowledge: the `anvil-agent-references` skills, issued directly by Anvil, which are how agents apply Anvil correctly; and `anvil-docs`, in `project-library-global`, a compilation of Anvil's own documentation without its images. Where two Anvil sources conflict, the conflict is raised to David, who resolves it; neither source silently wins. Standards and instructions form one consistent whole: a conflict between them is a defect, fixed at its source.

One GBrain search covers all of this knowledge, because every documentation repository is a GBrain source. Every step starts with a GBrain search, and the actual file a search points to is read before it is applied. New knowledge enters GBrain only through close-out and `mb-submit-memory`. PDLF may propose changes to `project-library-global` when a lesson concerns Anvil or application standards, and David approves them.

**Skills.** PDLF consists only of the skills that best serve its objectives: nothing superfluous and nothing lacking. Its skills come from GStack, Matt Pocock, Magdoub's wireframe skills and Anvil's `anvil-agent-references`. The skills catalog in `mybizz-os-docs` is their single register. A skill joins PDLF only if it earns its place; once there, it is always used for its task, and the agent never improvises a task a skill covers. Which skill each step uses is decided when that step is designed.

**Learning and self-healing.** PDLF must never learn the same lesson twice or repeat a mistake. Each lesson is written once, into the source that will actually be read next time: a lesson about Anvil or about good applications goes into `project-library-global`; a lesson about how PDLF works goes into the step, rule or specification concerned; a lesson about one application goes into that application's own documentation. When a step fails, or David corrects something, PDLF proposes the fix to that source, David approves it, and the fact is recorded in GBrain through `mb-submit-memory`. How each step learns is part of that step's design. Why: a lesson kept in a log is a lesson nobody reads.

**The ledger.** PDLF keeps one database record of every build: database `pdlf` on the Windows PostgreSQL 15 server, port 5433. It holds seven tables: projects, steps, gates, deviations, BFT records, ISC records and triage findings. The ledger is control, not ceremony: it lets the orchestrator refuse to pass a gate that was never approved, and lets a build resume or re-enter where it left off. Its connection details live in `.env`, which never leaves the computer. Detail: [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md). An application built by PDLF needs no judgement trail of its own: the ledger records every gate and deviation, and every step explains itself in plain language.

**Close-out and commits.** Close-out is the mybizz-os skill `/mb-close-out`, run when David asks for it. Only David commits and pushes, using `commit-all`; agents never do.

**What PDLF refuses.** Ceremony: reports and logs nobody reads, duplicate records, steps that exist only to look careful (stops and checks are not ceremony; they are how David controls the build). Unearned skills. Silent decisions. Shared databases.

**What success means.** PDLF succeeds when it is perpetually learning and self-healing, so that the development lifecycle is stable and dependable; when Anvil's standards are applied throughout every application it builds; and when it consists only of the skills that best serve its objectives. These claims are earned by real builds, starting with the test application, not by design alone.

### 7. The documents and their life cycle

Every PDLF document has one job, and a fact lives in only one of them.

- **This system build plan** holds what applies to PDLF as a whole. It is forward-looking.
- **Each step's build plan** (`NN-build-plan.md`, in the step's phase folder) holds that step's design while it is being worked out. When a step is taken up for design, its entry below moves into its own build plan and is removed from this one, so that any content lives in one place at a time.
- **When a step is built,** its build plan is turned into three documents, the same pattern as the rest of mybizz-os: `NN-config.md` (agent-facing: the step's fixed values, such as its inputs, outputs, file paths, skills, gate and BFT level); `NN-reference.md` (agent-facing: what the agent does, in order); and `NN-explainer.md` (for the agent and for David: what the step is, how it works and why). Its decision tree (`NN-decision-tree.html`) stays beside them, as the picture of the reference, and is kept matching it. The step's module is compiled from these files. The step's build plan then moves to `obsolete/`. A fact lives in only one of the three documents.
- **The step documents are functional, not historical.** They describe the step as it is, never how it came to be.
- **The built report** (`pdlf-library/docs-local/pdlf-built-report.md`) is the historical account of PDLF's own development, and only of PDLF, never of the applications PDLF builds. Entries are only ever added, never edited. Any history worth keeping goes there.
- **When the last step is built,** this plan is retired to `obsolete/`. Its system-wide content moves into small, single-subject documents in `pdlf-library/docs-local/`.
- **The older step material** (the existing step files, build notes and the `stepwise` folder) stays in place as source material. It is drawn on when each step is designed, and is not changed before then.

Why: each step is complex enough to need its own plan, and one plan for every step would grow too large to work with. A plan that dissolves into the step's own documents as the step is built leaves nothing behind to drift.

### 8. Rules every step follows

Every step is built to these rules. They are stated once here and not repeated in each step. Every step follows [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md), applies [[[pdlf:pdlf-library/specifications-local/spec-bft|Spec: BFT]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md), and names things per [[[default:specifications-global/spec-nomenclature|Spec: Nomenclature]]](C:/dev/project-library-global/specifications-global/spec-nomenclature.md). References that apply to particular steps are named at those steps.

- **It starts with a GBrain search** of the sources it needs, named explicitly (normally `{slug}`, `{slug}-project-library` and `project-library-global`), and it reads the actual file a search points to before applying it.
- **The developer approves every change.** The step explains each decision in plain language, never jumps a gate, and never passes one without the developer's approval.
- **Skills take precedence.** When a skill in PDLF's library covers a task, the step uses it and does not improvise.
- **Deviations are decided by the developer.** If the step cannot be done as written, it stops, sets out the options and what each costs, and the developer decides. The decision is recorded in the ledger.
- **It leaves its record:** a row in the ledger, its BFT record at its level, and a Step Receipt at `dev-{slug}\{slug}-project-library\pdlf\step-NN-receipt.md`.
- **Every artifact goes to its canonical place,** with a copy in `C:\pdlf\output\` for the developer's convenience.
- **The agent never commits or pushes.** Close-out is `/mb-close-out`, run when the developer asks for it; new knowledge reaches GBrain only through close-out and `mb-submit-memory`.
- **No application is ever multi-tenant.** Every step that shapes data or code keeps each client's application and database separate.

### 9. What is still to be settled

- **Steps work:** the orchestrator's form and its `opencode.json`; where entry points 06, 07 and 08 join the pipeline; which gates exist, where they sit and what each approves; the place and weight of the BFT thinking checkpoints; which `project-library-global` standard each step applies; whether applications receive a `CLAUDE.md`; the steps that build the remaining apps in `phase-g`; and the design of every step, one at a time, with Steps 42 to 44 rebuilt around the `develop` → `stable` release. The detailed list is kept in [[[pdlf:pdlf-library/docs-local/pdlf-todo|Active PDLF To-Do List]]](C:/pdlf/pdlf-library/docs-local/pdlf-todo.md).
- **The Cupcake proof:** once the orchestrator exists, an agent deliberately attempts to pass a gate without approval, and Cupcake must block it.
- **Testing:** designed as a component of its own, starting from a review of the testing disciplines.

---

## The Build Plan

### Phase A — Init

#### Step 1: Orchestrator

**Must achieve:** started by `/pdlf-init`, offers David the entry points in Steps 2 to 10, establishes the application (and, where it applies, the step to start from), runs the health check for an existing app, then runs the selected steps in order and stops at every gate for David's approval (section 4).

**Carried out by:** OpenCode, as the orchestrator. Designed in parts, alongside the steps it runs.

#### Steps 2 to 10: Entry points

**Must achieve:** one entry point each, as listed in section 4: 02 `new-app-no-context`, 03 `new-app-with-context`, 04 `add-feature-main-app`, 05 `update-main-app`, 06 `compile-master-template`, 07 `create-client-template`, 08 `create-management-app`, 09 `add-feature-management-app`, 10 `update-management-app`. Each is designed when its path through the pipeline is designed.

### Phase B — Discover and Define

Ends with the gate `domain-locked` (Step 16).

#### Step 11: Init

**Must achieve:** a sound foundation for the application: its code and documentation repositories exist, are linked to GitHub and registered in GBrain, the documentation repository has the standard folder structure, and the application has its record in the ledger. Works for a new application and for an existing one.

**Starts from:** the developer's answers (new or existing; the slug; the GitHub repository addresses, and for an existing application the local paths); the project template at `C:\dev\project-template\dev-(SLUG)\`; the ledger.

**Produces:** the code repository `dev-{slug}\{slug}\` and the documentation repository `dev-{slug}\{slug}-project-library\`, both linked to GitHub; their GBrain sources, `{slug}` and `{slug}-code`; the `projects` row in the ledger; for a new application, the three pre-project files in `pre-project\`.

**Carried out by:** OpenCode.

**Must be built so that:**
- it asks first whether the application is new or existing, and runs one procedure for both, differing only in how the repositories are obtained and checked;
- the code repository always comes from Anvil, which creates it when the app is created; the agent never creates it, and asks the developer to create the app first if there is no address yet;
- the documentation repository is created on GitHub only with the developer's permission;
- for an existing application, only genuinely missing folders are created, nothing existing is changed, and broken links or registrations are corrected only with permission;
- global reference files are never copied into the project; they are referenced where they live;
- it checks the ledger is reachable with all seven tables, and that `project-library-global` is registered in GBrain;
- it ends with a self-audit that reports any error and corrects nothing without permission.

**BFT level:** Full.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md), [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md).

#### Step 12: Office hours

**Must achieve:** the application's design doc: what problem it solves, for whom, and how, stated well enough for every later step to build on.

**Starts from:** for a new application, the three pre-project files; for an existing application, its whole existing documentation, read through GBrain.

**Produces:** `docs-local\design-doc-first-concept.md`, written once and never changed afterwards, kept to check later for concept drift; `docs-local\design-doc.md`, the working copy; the `/office-hours` result, if it ran.

**Carried out by:** OpenCode, with GStack `/office-hours` if the developer chooses.

**Must be built so that:**
- for a new application, the agent questions the developer until the scope is adequately described;
- for an existing application, the agent separates the durable concept from what merely followed from it, shows plainly any document that already claims to state the concept, and proposes the split for the developer to confirm or correct; the application is redeveloped around its concept, not audited;
- the design doc is always written, in a fixed structure (problem, demand, status quo, target user, constraints, approaches, recommendation, open questions, success criteria), before `/office-hours` is offered;
- if the developer accepts `/office-hours`, the full draft is pasted into it, so that it skips its interview but still challenges the premise and the alternatives; its result becomes the working copy, and its own file is never moved;
- the ledger records whether the design doc was synthesized without `/office-hours`, so that later steps carry an input notice;
- it hands four items to Step 14: both design docs, the `/office-hours` result if any, and its Step Receipt.

**BFT level:** Full.

**References:** [[[pdlf:pdlf-library/policy-local/pol-step-conditional-state|Step Conditional State Policy]]](C:/pdlf/pdlf-library/policy-local/pol-step-conditional-state.md).

#### Step 13: Not used

This step number is not used.

#### Step 14: CEO review

**Must achieve:** the design's scope and ambition challenged and settled, with the developer choosing how far the scope goes; the result is the CEO plan, which also names what must be tested and why.

**Starts from:** the four items handed over by Step 12; `project-library-global`.

**Produces:** the CEO plan, with a stable copy in the project.

**Carried out by:** GStack `/plan-ceo-review`.

**Must be built so that:**
- all four items from Step 12 are pasted into the skill in full, whatever route Step 12 took, with a plain statement that a design doc already exists, so that the skill does not reopen Step 12's decision by offering `/office-hours` again;
- before the skill runs, OpenCode compares what the review touches with `project-library-global`: the global standard wins unless the developer approves a deviation;
- the developer chooses the scope mode (expansion, selective expansion, hold scope or reduction), and every finding is put to the developer one at a time, never in a batch;
- the plan is captured in every mode: the skill saves it itself only in the two expansion modes, so in the other two OpenCode saves it;
- Step 12's input notice is carried forward if its design doc was synthesized.

**BFT level:** Full.

**References:** [[[pdlf:pdlf-library/policy-local/pol-step-conditional-state|Step Conditional State Policy]]](C:/pdlf/pdlf-library/policy-local/pol-step-conditional-state.md).

#### Step 15: Engineering review

**Must achieve:** the plan's architecture, code quality, test coverage and performance locked, and a concrete test plan produced for the build steps.

**Starts from:** Step 14's plan; both design docs; the `/office-hours` result, if any; `project-library-global`.

**Produces:** the reviewed plan and the test plan, with stable copies in the project. The test plan is used later by Steps 35 and 38.

**Carried out by:** GStack `/plan-eng-review`.

**Must be built so that:**
- Step 14's plan is found according to the scope mode used, and pasted into the skill in full with the design docs and the same statement that a design doc already exists;
- OpenCode makes the same comparison with `project-library-global` as at Step 14;
- the skill's scope challenge stops for the developer when the plan is large (8 or more files, or 2 or more new services);
- each finding in the four reviews (architecture, code quality, tests, performance) is put to the developer one at a time;
- the second opinion from another AI is informational only: nothing from it is adopted without the developer's approval;
- the findings are captured by OpenCode itself, so the step does not depend on the skill finding a plan file to write into.

**BFT level:** Full.

#### Step 16: Domain modeling

**Must achieve:** the application's vocabulary fixed, so that a term means the same thing in every later step, and the decisions that are hard to reverse recorded, before Phase C builds on them.

**Starts from:** Step 15's plan and test plan; for an existing application, its existing `CONTEXT.md`, decision records and code, marked as prior material.

**Produces:** `CONTEXT.md` (the glossary) and any decision records in `adr-local\`, in the documentation repository.

**Carried out by:** Matt Pocock `/grill-with-docs`, which runs a `/grilling` interview using `/domain-modeling`.

**Must be built so that:**
- the skill is told the project's own file locations, in place of its defaults;
- the interview settles one decision at a time, gives a recommended answer and waits for the developer; each settled term is written to `CONTEXT.md` at once, as a glossary only, with no implementation detail;
- a decision record is offered only for a decision that is hard to reverse, surprising without context and the result of a real trade-off;
- for an existing application, what the documents say is checked against the code, and contradictions are shown to the developer;
- the security review `mb-sentinel-review` checks for sensitive data or security-relevant entities before the gate; a finding stops the step and goes to the developer; the review's record in the ledger is checked, so that its run is proven, not assumed.

**BFT level:** Full (gate).

**Gate:** `domain-locked`: the vocabulary and decisions are locked; no new terms without reopening the gate.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

### Phase C — Design and Plan

Ends with the gates `concept-locked` (Step 21) and `wireframes-approved` (Step 26).

#### Step 17: Create Anvil data tables

**Must achieve:** The data tables are built in Anvil from the domain model and the ADRs.

**Carried out by:** The developer, by hand in the Anvil editor.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to schema construction
2. Developer: Build data tables/schema in Anvil IDE — Per ADRs and authoritative schema from Steps 15–16
3. Verify tables exist — STOP if missing
4. Write Step 17 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-17-receipt.md`
6. Apply BFT — Light level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 18: Pull to local

**Must achieve:** The code repository is pulled to local after the tables are built.

**Carried out by:** The developer, by hand.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to codebase state
2. Pull Anvil-connected code repo to local — Updated schema from Step 17
3. Verify local repo updated — STOP if schema not present
4. Write Step 18 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-18-receipt.md`
6. Apply BFT — None
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 19: To tickets

**Must achieve:** Breaks the plan into features (tickets) in the order they depend on each other. This is the feature list the build loop works through.

**Carried out by:** Matt Pocock, using `to-tickets`.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to issue decomposition
3. Read Step 14 CEO plan — `<project-library>/gstack-outputs/step-14-ceo-plan.md` (refined by Step 15)
4. Read CONTEXT.md + ADRs from Step 16
5. Confirm issue tracker config — From `/setup-matt-pocock-skills`
6. Invoke Matt `to-tickets` — Breaks spec into tracer-bullet issues in dependency order
7. Verify outputs — Issues published to project issue tracker; STOP if missing
8. Write Step 19 ledger row — `completed_at`
9. Generate Step Receipt — `<project-library>/pdlf/outputs/step-19-receipt.md`
10. Apply BFT — Full level
11. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 20: Design consultation

**Must achieve:** Builds the application's design system (`DESIGN.md`) on Material 3 and David's design standards. In a test run, the developer may abbreviate or skip it.

**Carried out by:** GStack, using `/design-consultation`.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to design system
2. Check test-mode flag — Present abbreviation offer (full/abbreviate/skip) if in test mode
3. Invoke GStack `/design-consultation` — Researches landscape, builds DESIGN.md + preview page
4. Verify outputs — DESIGN.md written, font/color preview page, design tokens; STOP if missing
5. Write Step 20 ledger row — `completed_at`
6. Generate Step Receipt — `<project-library>/pdlf/outputs/step-20-receipt.md`
7. Apply BFT — Full level
8. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 21: Concept sanity audit

**Must achieve:** Cross-checks everything produced so far for contradictions and reports the verdict.

**Carried out by:** OpenCode.

**Gate:** `concept-locked`: the concept is locked; no new feature without reopening the gate.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to cross-artifact consistency
2. Read all Phase B+C outputs — CEO review (Step 14), Eng review (Step 15), CONTEXT.md + ADRs (Step 16), DESIGN.md (Step 20)
3. Cross-reference each document pair for contradictions
4. Produce audit report — What was checked, findings, discrepancies, verdict
5. Save audit report — `<project-library>/pdlf/step-21-concept-audit.md`
6. Execute gate procedure — per `specifications-local/spec-gate-procedure.md`
7. Gate: `concept-locked` — Full BFT, gate summary, developer approval required; no new feature without formal gate reopening
8. Write Step 21 ledger row — `completed_at`
9. Generate Step Receipt — `<project-library>/pdlf/outputs/step-21-receipt.md`
10. Apply BFT — Full (gate override)
11. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 22: Wireframes, phase 1

**Must achieve:** Produces the structural wireframes, in black and white.

**Carried out by:** The Magdoub wireframe skill.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to wireframe generation
2. Invoke Claude Wireframe Skill (Magdoub) — Phase 1: 5 B&W UX wireframe approaches
3. Verify outputs — `wireframe/brain/design-context.md`, `design-taste.md`, `wireframe/DDMM-{feature}/index.html` + `styles.css`; STOP if missing
4. Write Step 22 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-22-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 23: Plan design review

**Must achieve:** Rates the design for usability and identifies gaps.

**Carried out by:** GStack, using `/plan-design-review`.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to design review
2. Invoke GStack `/plan-design-review` — Rates UX dimensions 0–10, identifies gaps
3. Verify outputs — GSTACK REVIEW REPORT appended to plan file; STOP if missing
4. Write Step 23 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-23-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 24: Plan developer-experience review

**Must achieve:** Reviews developer-experience friction in the plan.

**Carried out by:** GStack, using `/plan-devex-review`.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to developer experience review
2. Invoke GStack `/plan-devex-review` — Reviews API/CLI/SDK friction points and onboarding time
3. Verify outputs — DX scorecard appended to plan file; STOP if missing
4. Write Step 24 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-24-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 25: Not used

This step number is not used.

#### Step 26: Wireframes, phase 2

**Must achieve:** Produces the polished wireframes.

**Carried out by:** The Magdoub wireframe skill.

**Gate:** `wireframes-approved`: the wireframes are approved and Phase C ends.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to wireframe refinement
2. Invoke Claude Wireframe Skill (Magdoub) — Phase 2: Clean + Polished color variants
3. Verify outputs — `styles-opt1.css` through `styles-opt5.css`; STOP if missing
4. Execute gate procedure — per `specifications-local/spec-gate-procedure.md`
5. Gate: `wireframes-approved` — Full BFT, gate summary, developer approval required to proceed beyond Phase C
6. Write Step 26 ledger row — `completed_at`
7. Generate Step Receipt — `<project-library>/pdlf/outputs/step-26-receipt.md`
8. Apply BFT — Full (gate override)
9. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 27: Screen production

**Must achieve:** Produces screens from the approved wireframes. Deferred: runs only if the developer asks for it.

**Carried out by:** OpenCode.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to screen production
2. Check deferral status — Skip unless explicitly requested by developer
3. If active: Produce screen HTML from approved wireframe (Step 26)
4. Apply wireframe fidelity checklist
5. Apply screen standard compliance checklist
6. Verify outputs — Screen HTML, both checklists; STOP if missing
7. Write Step 27 ledger row — `completed_at` (or `deferred`)
8. Generate Step Receipt — `<project-library>/pdlf/outputs/step-27-receipt.md`
9. Apply BFT — Full level (if active)
10. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 28: Screen to PNG

**Must achieve:** Converts the screens to images. Deferred: runs only if the developer asks for it.

**Carried out by:** An external tool.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to screen conversion
2. Check deferral status — Skip unless explicitly requested by developer
3. If active: Convert screen HTML from Step 27 to PNG via external rendering tool
4. Verify output — Screen PNG in same folder as Step 27; STOP if missing
5. Write Step 28 ledger row — `completed_at` (or `deferred`)
6. Generate Step Receipt — `<project-library>/pdlf/outputs/step-28-receipt.md`
7. Apply BFT — None
8. Follow execution sequence — Housekeeping, stop, wait for continue

### Phase D — Scaffold and Assemble

Ends with the gate `architecture-verified` (Step 34).

#### Step 29: Build UI forms

**Must achieve:** The forms are built in Anvil from the approved wireframes.

**Carried out by:** The developer with Anvil's AI, by hand in the Anvil editor.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to UI form construction
2. Developer + Anvil AI: Build UI forms in Anvil IDE — From approved wireframes and screens
3. Verify forms exist in Anvil IDE — STOP if missing
4. Write Step 29 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-29-receipt.md`
6. Apply BFT — Light level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 30: Pull to local

**Must achieve:** The code repository is pulled to local after the forms are built.

**Carried out by:** The developer, by hand.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to codebase state
2. Pull Anvil-connected code repo to local — Component tree with Anvil AI's wiring
3. Verify local repo updated — STOP if UI forms not present
4. Write Step 30 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-30-receipt.md`
6. Apply BFT — None
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 31: Scaffold planning

**Must achieve:** Plans the modules and functions the code needs, as empty stubs, in `scaffold-plan.md`.

**Carried out by:** OpenCode.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to module/function structure planning
2. Review Step 15/16 architecture and domain model — TDD cluster, CONTEXT.md, ADRs
3. Review Step 30 pulled UI form structure
4. Review Step 21 concept audit report
5. Plan module/function structure — Determine what stubs to create
6. Write `scaffold-plan.md` — Saved to `<project-library>/`
7. Verify output — `scaffold-plan.md` exists; STOP if missing
8. Write Step 31 ledger row — `completed_at`
9. Generate Step Receipt — `<project-library>/pdlf/outputs/step-31-receipt.md`
10. Apply BFT — Full level
11. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 32: Physical scaffold build

**Must achieve:** The empty modules and functions are created in Anvil from the scaffold plan.

**Carried out by:** The developer, by hand in the Anvil editor.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to scaffold construction
2. Developer: Create empty client-code modules and server modules/functions in Anvil IDE — Per `scaffold-plan.md`
3. Verify stubs exist in Anvil IDE — STOP if missing
4. Write Step 32 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-32-receipt.md`
6. Apply BFT — Light level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 33: Pull to local

**Must achieve:** The code repository is pulled to local after the scaffold is built.

**Carried out by:** The developer, by hand.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to codebase state
2. Pull Anvil-connected code repo to local — Scaffold structure
3. Verify local repo updated — STOP if stubs not present
4. Write Step 33 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-33-receipt.md`
6. Apply BFT — None
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 34: Architectural sanity audit

**Must achieve:** Checks the tables, forms and scaffold against the locked decisions, so that nothing has drifted before any code is written.

**Carried out by:** OpenCode.

**Gate:** `architecture-verified`: the structure is verified and coding may begin.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to architecture verification
2. Compare actual Anvil data tables against ADRs and domain model — Every table/column traces to a locked decision
3. Compare actual UI forms against approved screens and DESIGN.md
4. Compare actual scaffolding against `scaffold-plan.md` — Every planned module/function exists, nothing improvised
5. Check for drift — If found, correct Anvil-side artifact or formally update plan/ADR per deviation mechanism
6. Produce audit report — What was checked, findings, discrepancies, verdict
7. Save audit report — `<project-library>/pdlf/step-34-architecture-audit.md`
8. Execute gate procedure — per `specifications-local/spec-gate-procedure.md`
9. Gate: `architecture-verified` — Full BFT, gate summary, developer approval required before any code-writing begins
10. Write Step 34 ledger row — `completed_at`
11. Generate Step Receipt — `<project-library>/pdlf/outputs/step-34-receipt.md`
12. Apply BFT — Full (gate override)
13. Follow execution sequence — Housekeeping, stop, wait for continue

### Phase E — Build and Verify

Steps 35 to 40B run once per feature, one feature at a time; the run plan governs the loop. Each feature ends with the gate `build-verified` (Step 39).

#### Step 35: Build

**Must achieve:** Builds one feature, tested at three levels: its logic alone, connected to the live Anvil app (with a backup before and after), and by hand in the browser. The developer signs the feature off.

**Carried out by:** OpenCode.

**Runs:** once per feature.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to this feature
2. Write the pure-logic function
3. Write Level 1 tests and run them locally
4. Decision point: Level 1 pass? Continue. Fail? Fix and retry
5. Create pre-integration backup
6. Write server-module (integration) wrapper
7. Write Level 2 tests
8. Push to Anvil — `git push` to branch, no auto-publish
9. Run Level 2 tests via Uplink against Development Environment
10. Decision point: Level 2 pass? Create post-success backup and continue. Fail? Restore from pre-integration backup, fix, retry
11. Pull repo back to local
12. Level 3: Manual/browser verification of complete feature
13. Decision point: Developer signoff on this feature
14. Generate Step Receipt for 35.N — `<project-library>/pdlf/outputs/step-35-{N}-receipt.md`
15. This feature is complete; the next feature starts again at Step 35 (the run plan governs the loop)
16. Follow execution sequence — Per cycle
17. Apply BFT — Full (per feature)

#### Step 35A: Testing

**Must achieve:** Broader testing of the feature, and a security check of the development and test tools (`pip-audit`).

**Carried out by:** OpenCode.

**Runs:** once per feature.

#### Step 36: Design review

**Must achieve:** A visual audit of the feature as it will ship, after any fixes from Step 40B.

**Carried out by:** GStack, using `/design-review`.

**Runs:** once per feature.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to visual audit
2. Invoke GStack `/design-review` — 80-item live-site visual audit; before/after screenshots, atomic fix commits
3. Verify outputs — Design audit report, screenshots, fix commits; STOP if missing
4. Write Step 36 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-36-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 37: Code review

**Must achieve:** Reviews the feature's code for bugs that would break in use. Findings are written to `step-37-findings.md`, including a clean-pass statement.

**Carried out by:** GStack, using `/review`.

**Runs:** once per feature.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to pre-landing code review
2. Invoke GStack `/review` — Finds bugs that pass CI but would break in production; auto-fixes obvious ones
3. Verify outputs — Review report, AUTO-FIXED commits; STOP if missing
4. Write Step 37 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-37-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 38: Quality testing

**Must achieve:** Tests the feature, and checks that earlier features still work. Findings are written to `step-38-findings.md`, including a clean-pass statement.

**Carried out by:** GStack, using `/qa`.

**Runs:** once per feature.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to QA testing
2. Invoke GStack `/qa` — Systematic QA testing; bug fixing; generates regression tests
3. Verify outputs — QA report with before/after screenshots, fix commits, regression test files; STOP if missing
4. Write Step 38 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-38-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 38A: Dependency check

**Must achieve:** Captures Anvil's own security check of the server packages, when the server environment was rebuilt.

**Carried out by:** OpenCode.

**Runs:** once per feature.

#### Step 39: Triage

**Must achieve:** Sorts the findings of Steps 37 and 38 for this feature.

**Carried out by:** Matt Pocock, using `triage`.

**Runs:** once per feature.

**Gate:** `build-verified`, for this feature: it is signed off and the next feature may start. Step 41 cannot begin until every feature has passed.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to issue triage
2. Invoke Matt `triage` — Updates issue tracker: comments, labels, state changes, agent briefs
3. Verify outputs — Labels applied, comments added, briefs written; STOP if missing
4. Write Step 39 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-39-receipt.md`
6. Apply BFT — Light level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 40: Architecture scan

**Must achieve:** An optional, read-only scan of the feature's code architecture. The developer decides for each feature whether it runs.

**Carried out by:** Matt Pocock, using `improve-codebase-architecture`.

**Runs:** once per feature.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to architecture health scan
2. Present RUN/SKIP recommendation with justification
   - Branch RUN: Invoke Matt `improve-codebase-architecture` — Interactive HTML architecture report
   - Branch SKIP: Skip the scan
3. Write Step 40 ledger row — `completed_at`
4. Generate Step Receipt — `<project-library>/pdlf/outputs/step-40-receipt.md`
5. Apply BFT — Full
6. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 40B: Approved fixes

**Must achieve:** Applies only the fixes the developer approved from Step 40. Skipped if Step 40 did not run or found nothing to fix.

**Carried out by:** OpenCode.

**Runs:** once per feature.

### Phase F — Ship and Monitor

Ends with the gates `production-released` (Step 44) and `released` (Step 46). Steps 42 to 44 still describe a staging and production split that PDLF does not have; they are rebuilt around the `develop` → `stable` release.

#### Step 41: Ship

**Must achieve:** Tests, versions and records the release, and pushes it; it stops at the push.

**Carried out by:** GStack, using `/ship`.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to ship readiness
2. Invoke GStack `/ship` — Tests, VERSION bump, CHANGELOG, commit, push; stops at push
3. Verify outputs — Merged base branch, tests pass, VERSION bumped, CHANGELOG updated, branch pushed; STOP if missing
4. Write Step 41 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-41-receipt.md`
6. Apply BFT — Light level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 42: Publish to staging

**Must achieve:** Still describes publishing to a staging environment, which PDLF does not have. To be rebuilt.

**Carried out by:** The developer, by hand.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to staging deployment
2. Developer: Publish the pushed commit to Staging environment in Anvil IDE — Production untouched
3. Verify output — App running at Staging URL; STOP if not reachable
4. Write Step 42 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-42-receipt.md`
6. Apply BFT — None
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 42A: Staging integration tests

**Must achieve:** Still describes a full integration test run on staging. To be rebuilt.

**Carried out by:** GStack and OpenCode.

#### Step 43: Staging smoke test

**Must achieve:** Still describes a smoke test on staging. To be rebuilt.

**Carried out by:** GStack, using `/qa` or `/canary`.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to staging verification
2. Invoke GStack `/qa` or `/canary` — Retargeted at Staging URL from Step 42
3. Verify output — Smoke test report: pass/fail at Staging; STOP if failing
4. Write Step 43 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-43-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 44: Release

**Must achieve:** Still describes promoting staging to production; to be rebuilt as the `develop` → `stable` release to `master_template`, which the developer performs.

**Carried out by:** The developer, by hand.

**Gate:** `production-released`: the application is released.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to production deployment
2. Developer: Promote the same reviewed commit from Staging to Production in Anvil IDE — Rollback is re-pointing, not `git revert`
3. Execute gate procedure — per `specifications-local/spec-gate-procedure.md`
4. Gate: `production-released` — Full BFT, gate summary, developer approval required; app is now live
5. Write Step 44 ledger row — `completed_at`
6. Generate Step Receipt — `<project-library>/pdlf/outputs/step-44-receipt.md`
7. Apply BFT — Full (gate override)
8. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 45: Production check

**Must achieve:** Watches the released application for errors and performance problems.

**Carried out by:** GStack, using `/canary`.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to post-deploy monitoring
2. Invoke GStack `/canary` — Targeted at Production URL from Step 44; watches for console errors, performance regressions
3. Verify output — Canary report with initial health check; STOP if critical failures
4. Write Step 45 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-45-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

#### Step 46: Learning

**Must achieve:** The retrospective: what this build taught is captured and written into the sources the next build reads.

**Carried out by:** OpenCode.

**Gate:** `released`: the build cycle closes.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to retrospective and learning
2. Invoke GStack `/retro` — Retrospective report
3. Invoke GStack `/learn` — Capture learnings
4. Invoke GStack `/context-save` — Persist working state
5. Update ISA — Fill Verification section, update Changelog
6. Update registry — `current_step: 46`, `last_gate: "released"`, `active: false`
7. Sync and embed GBrain — Learnings now searchable for next project
8. Execute gate procedure — per `specifications-local/spec-gate-procedure.md`
9. Gate: `released` (jointly with Step 45) — Full BFT, gate summary, developer approval required to close the project cycle
10. Write Step 46 ledger row — `completed_at`
11. Generate Step Receipt — `<project-library>/pdlf/outputs/step-46-receipt.md`
12. Apply BFT — Full (gate override)
13. Follow execution sequence — Housekeeping, stop

### Phase G — Remaining apps

**Must achieve:** the steps that build the rest of the five-app set in the same pipeline: `blank_client_template`, the first client instance with the provisioning procedure and the README every instance carries, and the management tooling. Not yet designed.
