---
title: "a01-build-plan"
doc-id: "mb-114d842c"
updated: "2026-10-29"
---
# Step 1 — Orchestrator: Build Plan

## Step entry

### Phase A — Init

Phase A has no gate. Its entry points join the pipeline at the steps the run order names.

#### Step 1: Orchestrator

**Must achieve:** one run of PDLF for one Mybizz business at a time, carried from its entry point through every step of its route, in order, resumed where it stopped whenever a session ends, and stopped for David at every step and gate, so that no step is skipped, repeated or run out of order and no gate passes without David.

**Starts from:** `/pdlf-init`, run by David in OpenCode opened in the business folder `C:\dev\dev-{slug}\`; the ledger; the run order, the routes and the built phases in this step's configuration; each entry point's configuration (Steps 2 to 10); each step's configuration, reference and test specification.

**Produces:** for each run, the entry point's `steps` row holding the entry record; for a new business, its `projects` row; an open `steps` row for every step as it starts; the run carried to its next step or paused at the first step whose phase is not yet built; the a01 test evidence in `{slug}-project-library\pdlf-outputs\a01\`.

**Carried out by:** OpenCode's Build agent, through the skill `pdlf-init`, started by David. David chooses the entry point, answers the entry questions, approves every step's outputs and records every gate's approval himself.

**Must be built so that:**
- David starts it with `/pdlf-init` in OpenCode opened in the business folder, `C:\dev\dev-{slug}\` (WSL `/mnt/c/dev/dev-{slug}`); the business slug is the folder's name without `dev-`; for a new business, David first creates the empty folder; PDLF itself is only read, never written, because no project data is kept in `C:\pdlf`;
- the skill `pdlf-init` is a thin launcher: it tells the agent to carry out this step's reference with this step's configuration, and, for every step the run reaches, that step's reference with its configuration and test specification under `spec-execution-discipline`; once a step's module is written, the module replaces the three; the skill's source is `C:\pdlf\pdlf-library\skills-local\pdlf-init\SKILL.md` and David installs it with one copy command;
- PDLF has no `opencode.json` of its own: the global configuration, the global `AGENTS.md` and Cupcake govern the agent, and OpenCode opened in the business folder may write only within it;
- when it starts, it confirms the ledger answers and the business folder is the working folder, then runs the resume check: it reads every run of the business from the ledger and, for each unfinished run, offers to continue it at the first step of its route that is not complete or skipped; David chooses to continue a run or to take a new entry point;
- a run whose next step lies in a phase not yet built is reported as paused at that step and is not offered, so the run is never begun again from the start and is resumed when the phase is built;
- it offers the entry points 02 to 10, and David chooses exactly one; the entry point asks its questions, checks the feature or update name is unused in the business and is never `app{n}`, runs the health check for an existing app, and writes the entry record into its own `steps` row; for entries 02 and 03 it first writes the `projects` row with the slug, the business's name and the mode, because every later row refers to it;
- it runs the steps of the run's route in order, and only steps of the built phases; before each step it checks the step's dependencies are complete and every gate before it is passed for the run, and stops with a deviation when one is not;
- every step opens its row with `status = 'in_progress'` at its start, so a run that stopped part-way through a step is resumed at that step;
- after every step it waits for David to run `/mb-close-out` and say "continue" before the next step, so every session ends at a step boundary;
- at a gate it presents the gate summary, gives David the `pdlf-gate.sh` command for the gate and run, waits, and reads the `gates` row; it never writes a gate row, and Cupcake's rule `no_agent_gate_approval` blocks any attempt;
- the routes, the dependencies and the built phases live once, in this step's configuration; each later phase adds its steps to them when it is built, and the orchestrator is extended with it.

**BFT level:** None for the orchestrator itself: it carries no judgement of its own. Each step it runs applies its own level, and every gate is Full.

**References:** [[[pdlf:app-factory/pdlf-build-plan|PDLF Build Plan]]](C:/pdlf/app-factory/pdlf-build-plan.md), sections 2, 4 and 5; [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md); [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md); [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md); [[[pdlf:pdlf-library/policy-local/pol-step-conditional-state|Step Conditional State Policy]]](C:/pdlf/pdlf-library/policy-local/pol-step-conditional-state.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `pdlf-init` (mybizz): starts the orchestrator → every step of the run.
- `writing-for-agents` (Matt Pocock): whenever `pdlf-init`'s `SKILL.md` is written or changed, because it is an instruction file for an agent → the orchestrator.

**Layers with no skill:** every layer of an application, because the orchestrator builds nothing itself: each step names its own skills.

**Testing:** [[[pdlf:app-factory/phase-a-init/a01-test-spec|Step 1 Test Specification]]](C:/pdlf/app-factory/phase-a-init/a01-test-spec.md): each entry joins at its step, a step with an incomplete dependency is refused, a run resumes where it stopped, and no gate passes without David.

**Standards:** [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md): the app each entry works on.

## Why it is built this way

- **Opened in the business folder.** Everything a run writes belongs to one business, and Cupcake lets an agent write only within the folder it was opened in. Opening OpenCode there gives the run exactly the reach it needs, and none into PDLF or another business.
- **A thin launcher.** The steps' configurations and references are the design; the skill only points the agent at them. While a phase is being proven, a correction to a step is a correction to its documents, and the launcher never changes.
- **The resume check first.** Each phase is proven by continuing the same `mb-3-cs` run, so the orchestrator must find where a run stopped, from the ledger alone, without David having to remember it.
- **An open row at every step's start.** A row written only at the end would leave a step that stopped part-way invisible; the open row makes it the step to resume.
- **Only built phases run.** A step whose documents are not yet built would be carried out from old drafts. Pausing there keeps the run on proven ground.
- **The entry record in the entry row.** Every step reads how the run began from one place, and an entry point that writes a row is itself a step that can be checked and resumed.
- **David records every gate.** A gate rests on David's decision, not on the agent's good behaviour; the script and the Cupcake rule make his command the only way a gate row can exist.
- **One home for the run order.** The routes and dependencies live only in this configuration, so the orchestrator and every step's dependency test read the same order.
