---
title: "pdlf-intent"
updated: "2026-10-10"
doc-id: "mb-ac926d36"
---
# PDLF — Statement of Intent

This document states what PDLF is for and what it must always be. It is the top layer of PDLF's documentation. Each section says what is intended and why, and points to the document that holds the detail. Where this document and another disagree, this document states the intent and the other is corrected.

---

## 1. What PDLF is

PDLF, the Project Development Lifecycle Framework, is an application development system. It builds Anvil.works applications.

PDLF is a system, not a project. It has no code repository of its own. It lives at `C:\pdlf` (GitHub `sassycomapp/pdlf`, private; GBrain source `pdlf`). All work on PDLF happens there; there is no other workshop or copy.

PDLF runs on mybizz-os, the operating system that supplies its memory, governance, documentation tools and close-out. The two are parts of one package: mybizz-os keeps the environment sound, and PDLF uses that environment to build applications.

Three names are never confused. **Mybizz** is the company. **mybizz-os** is the operating system. **PDLF** is the system that builds Mybizz's applications. Each application PDLF builds is its own Mybizz business.

The credo for PDLF, and everything in it, is: **simple, secure, robust, fit for purpose.**

## 2. Whom PDLF serves

PDLF serves David, the developer, and his collaborators: Claude and the OpenCode agent.

David is a project manager acting as developer. He reads code but is not a programmer, so he depends on PDLF and its agents to make the code correct. That fact shapes everything else in this document: PDLF carries the responsibility for correct code, and it explains every decision to David in plain language, so that he stays in control without having to judge code himself.

## 3. Control

PDLF never runs on its own. The orchestrator is David's tool for building an application, not an autonomous agent.

- Every change PDLF makes needs David's approval, until David says that a particular approval is no longer needed.
- More interaction is preferred to less. Interaction can be reduced later, as confidence in PDLF grows; it is never reduced by PDLF itself.
- The gates are absolutely essential. A gate is a hard stop where David approves a commitment before anything builds on it. PDLF never passes a gate without that approval.
- PDLF never oversteps or jumps a gate. Cupcake, the policy engine of mybizz-os, enforces this. That it does so while PDLF runs must be proven by test, not assumed.
- PDLF runs under the same rules as all OpenCode work: the global `AGENTS.md` and Cupcake. It has no separate rule system of its own.
- When a step cannot be done as written, the agent stops, sets out the options and what each one costs, and David decides. The decision is recorded.

Why: an AI agent left to itself drifts, skips steps and decides things nobody asked it to decide. David cannot catch that by reading code. Control has to be structural: built into how PDLF runs, not left to the agent's good behaviour.

Detail: [[[pdlf:pdlf-library/policy-local/pol-sequential-enforcement-and-deviation|Policy: Sequential Enforcement and Deviation]]](C:/pdlf/pdlf-library/policy-local/pol-sequential-enforcement-and-deviation.md), [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md), the global `AGENTS.md`.

## 4. What PDLF builds

PDLF builds many Anvil applications. Each is a separate business of Mybizz.

Every application follows the five-app structure ([[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md)):

| App | Role |
|---|---|
| App 1 | The development workspace, where all application code is written. |
| App 2 | `master_template`, the published dependency every client instance runs on. |
| App 3 | `blank_client_template`, the schema-only source from which client instances are cloned. |
| App 4 | Client instances, one per paying client, each with its own separate database. |
| App 5 | The management tooling for that business. |

Each business has its own dedicated set of five apps. `mb-3-cs` (Mybizz CS, consulting and services) has one set; `mb4ecom` (e-commerce) will have another.

**No application is ever multi-tenant.** This is permanent and sealed by [[[default:adr-global/adr-dependency-based-not-multi-tenant|ADR: Dependency-Based, Not Multi-Tenant]]](C:/dev/project-library-global/adr-global/adr-dependency-based-not-multi-tenant.md). Every client has its own application instance and its own database. No application ever shares one database between clients and separates them by filtering. This rule has no exceptions, and AI agents are given it as context before any code is generated, because they reach for shared-database patterns by default.

**Design.** Every application uses Anvil's Material 3 theme and David's design standards in `project-library-global`. Design moves in approved stages: structural wireframes, then polished wireframes, then screens. David approves each stage before the next begins.

**Quality.** Every feature is built, tested and signed off by David before the next feature begins. The findings of every review and QA pass are written to a file; a review that left no file did not happen. How PDLF tests is a subject of its own, designed separately.

## 5. Where PDLF's job begins and ends

**Begins.** David chooses an application and starts the orchestrator. The orchestrator asks him questions to establish what kind of work this is, and so where to begin:

- a new application starts at Step 11;
- a new feature for an existing application starts at an entry point reserved in Steps 2 to 10;
- an update or upgrade starts at another of those entry points;
- returning to one of the other apps of an existing five-app set starts at another.

The entry points in Steps 2 to 10 are designed in steps work. A new application with no prior context starts from three pre-project files: a brief, scoping ideas, and constraints and notes. An existing application brings its own context.

**Ends.** PDLF builds the entire five-app structure of a business in one continuous pipeline, so that the five apps stay consistent with each other. It releases the application to `master_template` through the `develop` → `stable` merge, which David performs as a gated step. For client instances, PDLF builds and verifies one instance (the first real client, also used as the test client), the provisioning procedure, and the README every instance must carry. Provisioning each later client follows that procedure as normal business operations, outside the build pipeline.

Why: the five apps depend on each other. Built separately, they drift apart; built in one pipeline, the decisions made for one are carried into the others.

**First builds.** A small test application, the Daily Intentions Tracker, goes through PDLF first, in `mb5pdlf`, so that PDLF's own faults are found cheaply. It can be extended if it proves too small to test PDLF fully. `mb-3-cs` follows, then the other Mybizz businesses.

## 6. Knowledge and standards

Each kind of knowledge has exactly one home, and a fact lives in only one of them:

| Home | Holds |
|---|---|
| `pdlf-library` (in `C:\pdlf`) | How PDLF itself works. |
| `project-library-global` (`C:\dev\project-library-global`) | What a good application is: Anvil knowledge, standards, specifications and decisions that apply to every application. It is project-agnostic and permanent. |
| A project's own `project-library`, `docs-local` | What is true of that one application only. |

Anvil's standards, specifications, principles and methods are applied throughout every application. Agents apply them using the skill set Anvil itself issues (`anvil-agent-references`). `project-library-global` also holds a compilation of Anvil's own documentation (`anvil-docs`, without images, which could not be downloaded). Where two Anvil sources conflict, the conflict is raised to David, who resolves it; neither source silently wins.

Standards and instructions form one integrated, consistent whole. There is never a contest over which wins: a conflict between them is a defect, fixed at its source.

One GBrain search covers all of this knowledge, because every documentation repository is a GBrain source.

Detail: [[[pdlf:pdlf-library/policy-local/pol-memory-and-knowledge|Policy: Memory and Knowledge]]](C:/pdlf/pdlf-library/policy-local/pol-memory-and-knowledge.md), [[[pdlf:pdlf-library/policy-local/pol-anvil-platform|Policy: Anvil Platform]]](C:/pdlf/pdlf-library/policy-local/pol-anvil-platform.md).

## 7. Learning and self-healing

PDLF must never learn the same lesson twice or repeat a mistake. It grows smarter, finer-tuned and more precise with every build.

- **Learning** means each lesson is written once, into the source that will actually be read next time. A lesson about Anvil goes into `project-library-global`. A lesson about how PDLF works goes into the relevant module, rule or specification in `pdlf-library`. A lesson about one application goes into that application's own `docs-local`.
- **Self-healing** means that when a step fails, or David corrects something, PDLF proposes the fix to that source, David approves it, and the fact is recorded in GBrain through `mb-submit-memory`.

Why: a lesson kept in a log is a lesson nobody reads. A lesson written into the source that the next build reads cannot be missed.

PDLF uses what already exists for this: GBrain, the ledger, governed memory and close-out. Established AI-engineering techniques are welcome where they fit. How each step learns is part of that step's design.

## 8. What PDLF refuses

**Ceremony.** Any process that does not serve the objective is not wanted: reports and logs nobody reads, duplicate records, steps that exist only to look careful. Stops and checks are not ceremony; they are how David controls the build, and they stay.

**Unearned skills.** PDLF uses only the skills that best serve its objectives: nothing superfluous, nothing lacking. A skill joins PDLF's library only if it earns its place; once there, it is always used for its task, and the agent never improvises instead.

**Silent decisions.** Nothing is decided without David, and nothing is skipped without a recorded decision.

## 9. What success means

PDLF succeeds when:

1. it is perpetually learning and self-healing, so that the development lifecycle is stable and dependable;
2. Anvil's standards are applied throughout every application it builds;
3. it consists only of the skills that best serve its objectives, with nothing superfluous and nothing lacking.

These claims are earned by real builds, starting with the test application, not by design alone.

## 10. Where the detail lives

| Subject | Document |
|---|---|
| How PDLF works | [[[pdlf:pdlf-library/pdlf-explainer-docs/pdlf-explainer\|PDLF Explainer]]](C:/pdlf/pdlf-library/pdlf-explainer-docs/pdlf-explainer.md) |
| The modules PDLF runs | [[[pdlf:pdlf-library/pdlf-explainer-docs/app-factory-explainer\|App Factory Explainer]]](C:/pdlf/pdlf-library/pdlf-explainer-docs/app-factory-explainer.md) |
| The orchestrator | [[[pdlf:pdlf-library/pdlf-explainer-docs/orchestrator-agent-explainer\|Orchestrator Agent Explainer]]](C:/pdlf/pdlf-library/pdlf-explainer-docs/orchestrator-agent-explainer.md) |
| The binding rules | [[[pdlf:pdlf-library/policy-local/pol-index\|Policy Index]]](C:/pdlf/pdlf-library/policy-local/pol-INDEX.md) |
| The steps | `stepwise/`, with `run-plan.md` (order) and `step-mapping.md` (what each step is) |
| The five-app structure | [[[default:specifications-global/spec-five-app-architecture-model\|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md) |
