---
title: "pdlf-intent"
updated: "2026-10-11"
doc-id: "mb-ac926d36"
---
# PDLF — Statement of Intent

This document states everything PDLF is meant to be: what it is, whom it serves, what it builds, how it runs, and what it must never become. It is the single statement of intent for the PDLF system and the top layer of its documentation. Every other PDLF document agrees with it. Where another document disagrees, this document states the intent and the other document is corrected. The document grows as PDLF grows: when a new intent is settled, it is written here.

---

## 1. What PDLF is

PDLF, the Project Development Lifecycle Framework, is an application development system. It builds Anvil.works applications.

PDLF is a system, not a project. It has no code repository of its own. It lives at `C:\pdlf` (WSL path `/mnt/c/pdlf`), in the private GitHub repository `sassycomapp/pdlf`, and its documents form the GBrain source `pdlf`, which covers the whole of `C:\pdlf`. All work on PDLF happens there. There is no workshop, no second copy and no separate development project: the earlier development project, makePDLF, was absorbed into PDLF and no longer exists.

PDLF runs on mybizz-os, the operating system that supplies its memory, governance, documentation tools and close-out. The two are parts of one package. mybizz-os keeps the environment sound; PDLF uses that environment to build applications.

Three names are never confused. **Mybizz** is the company. **mybizz-os** is the operating system. **PDLF** is the system that builds Mybizz's applications. Each application PDLF builds is its own Mybizz business.

The credo for PDLF, and for everything in it, is: **simple, secure, robust, fit for purpose.** Nothing is kept for ceremony, and nothing is kept for posterity.

## 2. Whom PDLF serves

PDLF serves David, the developer, and his collaborators: Claude and the OpenCode agent.

David is a project manager acting as developer. He reads code but is not a programmer, so he depends on PDLF and its agents to make the code correct. That fact shapes everything else in this document. PDLF carries the responsibility for correct code, and it explains every decision to David in plain language, so that he stays in control without having to judge code himself.

## 3. Control

PDLF never runs on its own. The orchestrator is David's tool for building an application, not an autonomous agent.

Every change PDLF makes needs David's approval, until David says that a particular approval is no longer needed. More interaction is preferred to less. Interaction can be reduced later, as confidence in PDLF grows, but only by David, never by PDLF itself.

The gates are absolutely essential. A gate is a hard stop at which David approves a commitment before anything is built on it. PDLF never passes a gate without that approval, and it never oversteps or jumps a gate. Cupcake, the policy engine of mybizz-os, enforces this. That Cupcake actually does so while PDLF runs must be proven by a deliberate test, not assumed.

PDLF runs under the same rules as all OpenCode work: the global `AGENTS.md` and Cupcake. It has no separate rule system of its own. Its access to each application's folders is set when the orchestrator is designed.

When a step cannot be done as written, the agent stops. It sets out the options and what each one costs, and David decides. The decision is recorded in the ledger. Nothing is skipped without a recorded decision.

Why: an AI agent left to itself drifts, skips steps and decides things nobody asked it to decide. David cannot catch that by reading code. Control therefore has to be structural, built into how PDLF runs, not left to the agent's good behaviour.

## 4. What PDLF builds

PDLF builds many Anvil applications. Each one is a separate business of Mybizz.

Every application follows the five-app structure set out in [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md). App 1 is the development workspace, where all application code is written. App 2 is `master_template`, the published dependency every client instance runs on. App 3 is `blank_client_template`, the schema-only source from which client instances are cloned. App 4 is the client instances, one per paying client, each with its own separate database. App 5 is the management tooling for that business. Each business has its own dedicated set of five apps: `mb-3-cs` (Mybizz CS, consulting and services) has one set, and `mb4ecom` (e-commerce) will have another.

**No application is ever multi-tenant.** This is permanent and sealed by [[[default:adr-global/adr-dependency-based-not-multi-tenant|ADR: Dependency-Based, Not Multi-Tenant]]](C:/dev/project-library-global/adr-global/adr-dependency-based-not-multi-tenant.md). Every client has its own application instance and its own database. No application ever shares one database between clients and separates them by filtering. This rule has no exceptions. AI agents are given it as context before any code is generated, because they reach for shared-database patterns by default.

**Design.** Every application uses Anvil's Material 3 theme and David's design standards in `project-library-global`. Design moves in approved stages: structural wireframes, then polished wireframes, then screens. David approves each stage before the next begins.

**Quality.** Every feature is built, tested and signed off by David before the next feature begins. Each feature is tested at three levels: its logic on its own, then connected to the live Anvil application, then by hand in the browser. The findings of every review and every quality check are written to a file; a review that left no file did not happen. How PDLF tests is designed as a component of its own (see section 14).

## 5. Where PDLF's job begins and ends

**Where it begins.** David chooses an application and starts the orchestrator. The orchestrator asks him questions to establish what kind of work this is, and therefore where the work begins. A new application starts at Step 11. A new feature for an existing application starts at an entry point reserved in Steps 2 to 10. An update or upgrade starts at another of those entry points. Returning to one of the other apps of an existing five-app set starts at another. The other four apps may later need maintenance entry points of their own; that is a thought, not yet a decision.

A new application with no prior context starts from three pre-project files: a brief, scoping ideas, and constraints and notes. The blank set of these three files is part of PDLF and ships with it, because more than one step reads it; it is kept current with the pipeline. An existing application brings its own context instead. Exactly how each kind of application enters is settled when Step 11 is designed.

**Where it ends.** PDLF builds the entire five-app structure of a business in one continuous pipeline, so that the five apps stay consistent with each other. Step 46 currently ends with `master_template`; the steps that build the remaining apps are added after it. PDLF releases the application to `master_template` through the `develop` → `stable` merge, which David performs as a gated step. There is no separate staging or production environment.

For client instances (App 4), PDLF builds and verifies one instance, the provisioning procedure, and the README every instance must carry. That first instance is the first real client, also used as the test client. Provisioning each later client follows the procedure as normal business operations, outside the build pipeline. App 5, the management tooling, is built in the same pipeline as the rest of that business's apps.

Why: the five apps depend on each other. Built separately, they drift apart; built in one pipeline, the decisions made for one are carried into the others.

**First builds.** A small test application, the Daily Intentions Tracker, goes through PDLF first, in `mb5pdlf`, so that PDLF's own faults are found cheaply, before they can damage a real business. Its filled-in pre-project files belong to `mb5pdlf`. It can be extended if it proves too small to test PDLF fully. `mb-3-cs` follows, then the other Mybizz businesses.

## 6. How PDLF runs

PDLF runs inside OpenCode, through the OpenCode Build agent and its model.

**The orchestrator** is a step: Step 1. It asks David the questions that establish the entry point, then runs the modules selected for that entry, in order, and stops at every gate. Its exact form is designed in steps work.

**Steps and modules.** Every step lives in `app-factory/`, in the folder of its phase: `phase-a-init` (1 to 10), `phase-b-discover-and-define` (11 to 16), `phase-c-design-and-plan` (17 to 28), `phase-d-scaffold-and-assemble` (29 to 34), `phase-e-build-and-verify` (35 to 40b) and `phase-f-ship-and-monitor` (41 to 46); a `phase-g` folder is added for the remaining apps when they are designed. A step's files are named by its number: `11-init.md` is the step itself. When a step is finished, it is compiled into its module file, `11-module.md`, in the same folder: a single, self-contained unit that holds the finished step and everything only that step needs. Until then the module file is a placeholder. Anything several modules need about how PDLF itself works lives once, in `pdlf-library`.

**Three documents steer the build.** `pdlf-build-plan.md`, at the top of `app-factory/`, is the blueprint: what each step must achieve and the rules every step is built to; it is retired to `obsolete/` when PDLF is built. `pdlf-built-report.md` (in `pdlf-library/docs-local/`) records what has been built, step by step, and is kept as the record of what PDLF consists of. `orchestrator-run-plan.md` (in `pdlf-library/docs-local/`) is the order in which the orchestrator runs the steps, including the per-feature loop. Which modules run depends on the entry point; not every step runs for every kind of work.

**Numbering.** The current step numbers are kept, because Steps 2 to 10 are reserved for entry points. Steps 13 and 25 are not used.

**Two repositories per application.** Every application has a code repository, which is the Anvil app itself, and a documentation repository, which holds everything else: documents, decisions and PDLF records. The two are never mixed. When an application re-enters PDLF later, PDLF reads both repositories directly; there is no third repository.

**What goes to Anvil.** Everything committed to the code repository is pushed to Anvil and stored there, so `.gitignore` keeps out everything that must stay local, such as `.env`, credentials and test output. Anvil uses only `anvil.yaml`, `client_code`, `server_code` and `theme`. Two parts are public: every file in `theme/assets` can be opened by anyone with its link, and the code in `client_code` runs in the user's browser, where it can be read. Nothing secret, internal or for paying clients only ever goes in either. Client-facing documents, such as user guides, may be served from `theme/assets/docs`. Explainer videos are hosted on YouTube and linked or embedded, because large video files would weigh down every repository. No agent ever writes `anvil.yaml`; Anvil manages it. The code repository is pulled to local after every step in which work was done in the Anvil editor.

**Instruction files.** `AGENTS.md` is PDLF's single instruction file; there is no `CLAUDE.md`. A PDLF `opencode.json` is written when the orchestrator is designed, because only then is it known what PDLF needs beyond the global settings.

**Artifacts.** Every artifact is written to its canonical place, and a copy is also written to `output/` for David's convenience. `output/` serves one application at a time; when an application ships, its copies are copied into that application's own folders, their arrival is verified, and only then is `output/` cleared.

## 7. Knowledge and standards

Each kind of knowledge has exactly one home, and a fact lives in only one of them:

- `pdlf-library` (in `C:\pdlf`) holds how PDLF itself works.
- `project-library-global` (`C:\dev\project-library-global`) holds what a good application is: Anvil knowledge, standards, specifications and decisions that apply to every application. It is project-agnostic and permanent, and it is the standard every application is built to.
- An application's own documentation repository (its `docs-local`) holds what is true of that one application only.

The one deliberate exception is nomenclature. All names are defined in a single document, [[[default:specifications-global/spec-nomenclature|Spec: Nomenclature]]](C:/dev/project-library-global/specifications-global/spec-nomenclature.md): one part for what is common, one part for PDLF, and one part for each application. A term is defined once.

Anvil's standards, specifications, principles and methods are applied throughout every application. There are two sources of Anvil knowledge. The `anvil-agent-references` skills, issued directly by Anvil, are how agents apply Anvil correctly. `anvil-docs`, in `project-library-global`, is a compilation of Anvil's own documentation, without its images, which could not be downloaded. Where two Anvil sources conflict, the conflict is raised to David, who resolves it; neither source silently wins.

Standards and instructions form one integrated, consistent whole. There is never a contest over which one wins: a conflict between them is a defect, fixed at its source.

One GBrain search covers all of this knowledge, because every documentation repository is a GBrain source. Every step starts with a GBrain search. The actual file a search points to is read before it is applied. New knowledge enters GBrain only through close-out and `mb-submit-memory`.

PDLF may propose changes to `project-library-global` when a lesson concerns Anvil or application standards, and David approves them. A lesson that is true of one application only goes to that application's own documentation, never to `project-library-global`.

## 8. Skills

PDLF consists only of the skills that best serve its objectives: nothing superfluous and nothing lacking. Its skills come from GStack, Matt Pocock, Magdoub's wireframe skills and Anvil's `anvil-agent-references`. The skills catalog in `mybizz-os-docs` is the single register of them. A skill joins PDLF's library only if it earns its place. Once it is there, it is always used for its task: when a skill in the library covers a task, the agent uses it and never improvises instead. Which skill each step uses is decided when that step is designed.

## 9. Learning and self-healing

PDLF must never learn the same lesson twice or repeat a mistake. It grows smarter, finer-tuned and more precise with every build.

**Learning** means each lesson is written once, into the source that will actually be read next time. A lesson about Anvil or about good applications goes into `project-library-global`. A lesson about how PDLF works goes into the module, rule or specification concerned. A lesson about one application goes into that application's own documentation.

**Self-healing** means that when a step fails, or David corrects something, PDLF proposes the fix to that source, David approves it, and the fact is recorded in GBrain through `mb-submit-memory`.

PDLF uses what already exists for this: GBrain, the ledger, governed memory and close-out. Established AI-engineering techniques are welcome where they fit. How each step learns is part of that step's design.

Why: a lesson kept in a log is a lesson nobody reads. A lesson written into the source that the next build reads cannot be missed.

## 10. Records

**The ledger.** PDLF keeps one database record of every build, the ledger: database `pdlf` on the Windows PostgreSQL 15 server, port 5433. It holds seven tables: projects, steps, gates, deviations, BFT records, ISC records and triage findings. The ledger is control, not ceremony: it is what lets the orchestrator refuse to pass a gate that was never approved, and what lets a build resume or re-enter where it left off. Its connection details live in `.env`, which never leaves the computer. Detail: [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md).

**No other trail.** An application built by PDLF needs no judgement trail of its own: the ledger records every gate and deviation, and every step explains itself in plain language.

**Close-out and commits.** Close-out is the mybizz-os skill `/mb-close-out`, run when David asks for it. It replaces the old end-of-step housekeeping questions. Only David commits and pushes, using `commit-all`; agents never do.

## 11. What PDLF refuses

**Ceremony.** Any process that does not serve the objective is not wanted: reports and logs nobody reads, duplicate records, steps that exist only to look careful. Stops and checks are not ceremony; they are how David controls the build, and they stay.

**Unearned skills.** No skill is kept that does not earn its place, and no task a skill covers is improvised.

**Silent decisions.** Nothing is decided without David, and nothing is skipped without a recorded decision.

**Shared databases.** No application is ever multi-tenant.

## 12. What success means

PDLF succeeds when it is perpetually learning and self-healing, so that the development lifecycle is stable and dependable; when Anvil's standards are applied throughout every application it builds; and when it consists only of the skills that best serve its objectives, with nothing superfluous and nothing lacking.

These claims are earned by real builds, starting with the test application, not by design alone.

## 13. Where PDLF lives

`C:\pdlf` holds the whole system. `AGENTS.md` and `README.md` sit at the top, beside `.env`, which is never committed. `app-factory/` holds the build: the phase folders with their step files and module files, and the build plan. `pdlf-library/` holds PDLF's own documentation: its explainers, policies, specifications, decision records, processes and templates. `output/` holds the artifact copies for the application currently being built, and is never committed. `obsolete/` holds retired documents. `desktop/` holds working files.

`AGENTS.md` carries three standing rules: all PDLF work happens in `C:\pdlf`; a module file is written only by compiling its step's files, on the developer's instruction; and `output/` serves one application at a time.

The detail of how PDLF works is in the [[[pdlf:pdlf-library/pdlf-explainer-docs/pdlf-explainer|PDLF Explainer]]](C:/pdlf/pdlf-library/pdlf-explainer-docs/pdlf-explainer.md), the [[[pdlf:pdlf-library/pdlf-explainer-docs/app-factory-explainer|App Factory Explainer]]](C:/pdlf/pdlf-library/pdlf-explainer-docs/app-factory-explainer.md), the [[[pdlf:pdlf-library/pdlf-explainer-docs/orchestrator-agent-explainer|Orchestrator Agent Explainer]]](C:/pdlf/pdlf-library/pdlf-explainer-docs/orchestrator-agent-explainer.md) and the binding rules listed in the [[[pdlf:pdlf-library/policy-local/pol-index|Policy Index]]](C:/pdlf/pdlf-library/policy-local/pol-INDEX.md).

## 14. What is still to be settled

The PDLF system is settled. What remains is designed in the order below, and each part is written into this document as it is settled.

**Steps work** comes next. It settles the orchestrator's form and its `opencode.json`; the entry points in Steps 2 to 10 and how the entry point selects which modules run; which gates exist, where they sit and what each approves; the place and weight of the BFT thinking checkpoints; how a new and an existing application each enter at Step 11, and whether applications receive a `CLAUDE.md`; which `project-library-global` standard each step applies; the steps that build the remaining apps after Step 46; and the rebuild of Steps 17 to 46, one at a time, with Steps 42 to 44 rebuilt around the `develop` → `stable` release. The detailed list is kept in [[[pdlf:pdlf-library/docs-local/pdlf-todo|Active PDLF To-Do List]]](C:/pdlf/pdlf-library/docs-local/pdlf-todo.md).

**The Cupcake proof.** Once the orchestrator exists, an agent deliberately attempts to pass a gate without approval, and Cupcake must block it. This is critical.

**Testing** is designed as a component of its own. The testing disciplines are reviewed first; then the testing standard is written for `project-library-global`, drawing on the philosophy of `anvil_cop_testing.md` and on David's further input, and `pol-testing-and-quality` is updated to match.

**The READMEs** of `pdlf-library` and `app-factory` are written last, once everything else is done.
