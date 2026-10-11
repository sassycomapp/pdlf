---
title: "pdlf-explainer"
doc-id: "mb-4ba5a053"
updated: "2026-10-11"
---
# PDLF — How It Works

This document explains how PDLF works: its parts, how a build runs, and why it runs that way. What PDLF is for, and what it must always be, is stated in [[[pdlf:pdlf-library/pdlf-explainer-docs/pdlf-intent|PDLF Statement of Intent]]](C:/pdlf/pdlf-library/pdlf-explainer-docs/pdlf-intent.md). Where the two seem to disagree, the statement of intent is right and this document is corrected.

---

## 1. The parts of PDLF

PDLF lives at `C:\pdlf`. It has five parts, and each does one job.

| Part | Where | What it does |
|---|---|---|
| The modules | `app-factory/` | One module per pipeline step. A module is a finished step, packaged as one unit. The modules are what actually runs. |
| The step design | `stepwise/` | Where each step is designed before it becomes a module. `run-plan.md` decides the order of steps; `step-mapping.md` says what each step is and who handles it. |
| The library | `pdlf-library/` | The machinery every module shares: specifications, policies, decisions (ADRs), processes, templates and these explainers. |
| The orchestrator | Step 1 (module 01) | Runs a build. It establishes where to begin, runs the modules in order, and stops for David at every decision. |
| The ledger | PostgreSQL database `pdlf` | PDLF's record of each build: steps done, gates passed, deviations decided. |

PDLF also depends on things it does not own:

- **OpenCode** runs PDLF. Every step is carried out by the OpenCode Build agent and its model.
- **mybizz-os** supplies memory (GBrain and governed memory), governance (the global `AGENTS.md` and Cupcake), documentation upkeep and close-out.
- **`project-library-global`** holds the standards every application is built to.
- **The skill library** supplies specialised skills from GStack, Matt Pocock, Magdoub and Anvil.

PDLF has one instruction file for agents, `C:\pdlf\AGENTS.md`, which sits under the global `AGENTS.md`. There is no `CLAUDE.md`. PDLF's own OpenCode settings file (`opencode.json`) is written when the orchestrator is designed.

## 2. How a build runs

### Starting

David chooses an application and starts the orchestrator in OpenCode. The orchestrator asks him what kind of work this is, and from his answers chooses the entry point:

| Work | Entry point |
|---|---|
| A new application | Step 11 |
| A new feature for an existing application | An entry point in Steps 2 to 10 |
| An update or upgrade of an existing application | An entry point in Steps 2 to 10 |
| Returning to another app of an existing five-app set | An entry point in Steps 2 to 10 |

Steps 2 to 10 are reserved for these entry points and are designed in steps work. A new application starts from three pre-project files that David supplies: a brief, scoping ideas, and constraints and notes. An existing application brings its own context, read from its two repositories.

### The pattern of every step

Every step follows the same pattern. The step's own file says *what* the step does; the orchestrator supplies *how* every step is carried out, identically:

1. **Search.** The step searches GBrain for what is already known about its subject.
2. **Read.** It reads the actual files the search points to, in full. A search result is a pointer, never the source.
3. **Do.** It does the step's work, using the skill the step names. If the work is David's (for example, building tables in the Anvil editor), it gives him exact instructions and waits.
4. **Verify.** It confirms the expected output really exists. If it does not, the step stops and raises a deviation (section 6).
5. **Think.** It answers the step's thinking checkpoint (BFT, section 8) for what just happened, specifically, never generically.
6. **Record.** It writes the step's row to the ledger and produces the Step Receipt from that row.
7. **Explain and stop.** It explains in plain language what was done and why, and waits for David.
8. **Close out.** It asks David to run `/mb-close-out`. Nothing is committed, pushed or written to memory without it.

Why the same pattern everywhere: a pattern written once and enforced by the orchestrator cannot be skipped by one step and forgotten by another. David only has to learn it once.

### Phases and gates

The pipeline runs in phases. Each phase ends at a gate: a hard stop where David approves a commitment before anything is built on it. The gates in the current step design are `domain-locked`, `concept-locked`, `wireframes-approved`, `architecture-verified`, `build-verified` (once per feature), `production-released` and `released`. Which gates exist, where they sit and why is settled in steps work; [[[pdlf:pdlf-library/docs-local/pdlf-built-report|Step Mapping]]](C:/pdlf/pdlf-library/docs-local/pdlf-built-report.md) holds the current list.

At a gate, the orchestrator presents a gate summary and waits for David's explicit yes or no. A passed gate is never silently undone; reopening it is a recorded decision. PDLF never passes a gate without David's approval, and Cupcake enforces this. The procedure is in [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

### Building features

Features are built one at a time, in a loop. Each feature is built, tested at three levels, reviewed and passed through its own `build-verified` gate before the next feature begins. The three levels are:

1. **Logic alone**: the feature's business rules, written without any Anvil code, tested on their own.
2. **Connected**: the feature tested against the live Anvil application through Anvil Uplink, with a backup taken before and after.
3. **By hand**: David tries the finished feature in the browser and signs it off.

Review and QA findings are always written to a file, including a statement when a review finds nothing; a claimed review that left no file did not happen. How PDLF tests is being designed as a subject of its own; until then, the current rules are in [[[pdlf:pdlf-library/policy-local/pol-testing-and-quality|Policy: Testing and Quality]]](C:/pdlf/pdlf-library/policy-local/pol-testing-and-quality.md).

### Finishing

PDLF builds the whole five-app structure of the business in one pipeline. It releases the application to `master_template` through the `develop` → `stable` merge, which David performs as a gated step. It then builds the remaining apps of the set, including one verified client instance, the provisioning procedure, and the README every client instance must carry. The steps after Step 46 that build the remaining apps are added in steps work.

## 3. The ledger

The ledger is PDLF's own PostgreSQL database, `pdlf`. It runs on Windows (PostgreSQL 15, port 5433); OpenCode runs in WSL and reaches it through PowerShell, as set out in [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md). The connection settings and passwords are in `C:\pdlf\.env`, which is never committed.

It holds seven tables: `projects`, `steps`, `gates`, `deviations`, `bft_records`, `isc` (the criteria for "done") and `triage_findings`.

Why it exists: it is control, not ceremony. Because every step, gate and deviation is a row, the orchestrator can refuse to run a step whose predecessors are not done, refuse to pass a gate that was never approved, and resume a build exactly where it stopped, in any later session. Only the orchestrator, carrying out a PDLF step, writes to it.

The Step Receipt that David reads after each step is produced from the ledger row that step just wrote. It is never written separately, so the report cannot differ from the record.

## 4. Knowledge

Knowledge has three homes, and each fact lives in only one of them:

- `pdlf-library` holds how PDLF works;
- `project-library-global` holds what a good application is, for every application;
- each project's own `project-library`, `docs-local`, holds what is true of that application only.

Every documentation repository is a GBrain source, so one search covers all three. New knowledge enters GBrain only through close-out and `mb-submit-memory`, with David's approval.

**Learning.** When a build teaches something, the lesson is written once, into the source the next build will read: an Anvil lesson into `project-library-global`, a lesson about PDLF into the module, rule or specification concerned, a lesson about one application into that application's `docs-local`.

**Self-healing.** When a step fails or David corrects something, PDLF proposes the fix to that source. David approves it, and the fact is recorded in GBrain through `mb-submit-memory`.

The rules are in [[[pdlf:pdlf-library/policy-local/pol-memory-and-knowledge|Policy: Memory and Knowledge]]](C:/pdlf/pdlf-library/policy-local/pol-memory-and-knowledge.md).

## 5. Skills

PDLF uses skills from four families:

| Family | Contributes |
|---|---|
| GStack | Structured reviews from different angles (scope, engineering, design, developer experience), QA in a real browser, code review, shipping. |
| Matt Pocock | Domain modelling (a locked shared vocabulary and decisions), turning the plan into tickets, triage of findings, architecture health. |
| Magdoub wireframe | Structural wireframes first, then polished wireframes. |
| Anvil (`anvil-agent-references`) | How Anvil itself works: server code, client forms, data models and the rest, issued by Anvil. |

The skills catalog in mybizz-os ([[[mybizz-os-docs:os-reference-docs/skills-catalog|Skills Catalog]]](C:/mybizz/mybizz-os-docs/os-reference-docs/skills-catalog.md)) is the single register of which skills are installed. Which skill each step uses is decided in that step's design.

When a skill in the library covers a task, the agent must use it; it never improvises the task itself. A skill joins the library only if it earns its place. Before invoking a skill, the agent reads the skill's own file, because a skill's name does not reliably say what it does. The rules are in [[[pdlf:pdlf-library/policy-local/pol-skill-invocation|Policy: Skill Invocation]]](C:/pdlf/pdlf-library/policy-local/pol-skill-invocation.md).

## 6. Deviations

When a step cannot be done as written, the agent never decides what to do. It stops and sets out the options, with what each one costs: an alternative action, resolving the blocker, or skipping the step with its consequence stated. David decides, and the decision is recorded in the ledger. The same applies when what the agent finds in the files disagrees with what David says is true: the disagreement is raised at once and settled as a deviation. The procedure is in [[[pdlf:pdlf-library/policy-local/pol-sequential-enforcement-and-deviation|Policy: Sequential Enforcement and Deviation]]](C:/pdlf/pdlf-library/policy-local/pol-sequential-enforcement-and-deviation.md).

## 7. Artifacts

Each step's outputs (plans, reviews, designs, reports) are written to their canonical place: inside the application's documentation repository, or where a skill saves by design. A copy of each is also written to `C:\pdlf\output/`, sorted by the tool that produced it, so David can find the current build's outputs in one place. `output/` serves one application at a time and is not kept in Git. The rules are in [[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md).

## 8. Thinking checkpoints (BFT)

At each step the agent answers a thinking checkpoint based on Edward de Bono's BODY Frame Thinking: what the essential structure is, what does the work, how the parts connect, what is unnecessary, how the result is presented, and whether it is sound. Steps with real decisions get the full set; mechanical steps get a short one or none; every gate gets the full set. A blank, generic or copied answer counts as no answer. The place and weight of these checkpoints are settled in steps work; the current rules are in [[[pdlf:pdlf-library/policy-local/pol-bft-discipline|Policy: BFT Discipline]]](C:/pdlf/pdlf-library/policy-local/pol-bft-discipline.md).

## 9. Close-out and Git

At the end of every step the agent asks David to run `/mb-close-out`, the mybizz-os close-out. It saves what must be remembered, processes the memory governor's review queue, updates the project's documents, and ends with David running `commit-all` in the WSL terminal, which commits every documentation repository, updates GBrain and pushes.

Agents never commit or push. This keeps every change to the permanent record in David's hands.

## 10. Anvil

PDLF builds for Anvil.works only. The rules are in [[[pdlf:pdlf-library/policy-local/pol-anvil-platform|Policy: Anvil Platform]]](C:/pdlf/pdlf-library/policy-local/pol-anvil-platform.md); the essentials are these.

- **Two repositories per application.** The code repository is the Anvil app (App 1, the development workspace). The documentation repository holds everything else. They are never mixed.
- **What goes to Anvil.** Everything committed to the code repository is pushed to Anvil; `.gitignore` keeps local-only material, such as `.env`, out. Anvil uses only `anvil.yaml`, `client_code`, `server_code` and `theme`. `theme/assets` and `client_code` are public, so nothing secret or internal goes there. Client documents may be served from `theme/assets/docs`; explainer videos are hosted on YouTube.
- **`anvil.yaml` is never written by an agent.** Anvil manages it.
- **No multi-tenancy, ever.** Every client has its own app instance and its own database. No code shares one database between clients and separates them by filtering. AI agents reach for that pattern by default, so it is given to them as context before any code is written: [[[default:adr-global/adr-dependency-based-not-multi-tenant|ADR: Dependency-Based, Not Multi-Tenant]]](C:/dev/project-library-global/adr-global/adr-dependency-based-not-multi-tenant.md).
- **Never add forms or server modules to a client instance.** A client instance runs on `master_template`; anything added directly to it silently and permanently cuts it off from future updates: [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md).
- **Material 3.** Every application uses Anvil's Material 3 theme and David's design standards in `project-library-global`. Design moves in approved stages: structural wireframes, then polished wireframes, then screens.

## 11. Where things live

| Subject | Document |
|---|---|
| What PDLF is for | [[[pdlf:pdlf-library/pdlf-explainer-docs/pdlf-intent\|PDLF Statement of Intent]]](C:/pdlf/pdlf-library/pdlf-explainer-docs/pdlf-intent.md) |
| The modules | [[[pdlf:pdlf-library/pdlf-explainer-docs/app-factory-explainer\|App Factory Explainer]]](C:/pdlf/pdlf-library/pdlf-explainer-docs/app-factory-explainer.md) |
| The orchestrator | [[[pdlf:pdlf-library/pdlf-explainer-docs/orchestrator-agent-explainer\|Orchestrator Agent Explainer]]](C:/pdlf/pdlf-library/pdlf-explainer-docs/orchestrator-agent-explainer.md) |
| Step order | [[[pdlf:pdlf-library/docs-local/orchestrator-run-plan\|Run Plan]]](C:/pdlf/pdlf-library/docs-local/orchestrator-run-plan.md) |
| What each step is | [[[pdlf:pdlf-library/docs-local/pdlf-built-report\|Step Mapping]]](C:/pdlf/pdlf-library/docs-local/pdlf-built-report.md) |
| The binding rules | [[[pdlf:pdlf-library/policy-local/pol-index\|Policy Index]]](C:/pdlf/pdlf-library/policy-local/pol-INDEX.md) |
| The execution sequence in detail | [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline\|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) |
| Configuration | [[[pdlf:pdlf-library/docs-local/config\|PDLF Configuration]]](C:/pdlf/pdlf-library/docs-local/config.md) |
