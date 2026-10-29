---
title: "a01-explainer"
doc-id: "mb-64791255"
updated: "2026-10-29"
---
# Step 1 — Orchestrator: Explainer

## What it is

The orchestrator is the agent that carries one Mybizz business through PDLF. It is Step 1, but it is not a step like the others: it is what runs them. It finds where the business's work stands, takes a new entry point when David starts new work, and runs the steps of the run one at a time, in order, stopping for David after every one.

The orchestrator never runs on its own. It is David's tool, and it stops wherever a decision belongs to him.

## How it works

David opens the business's App 1 repository, `projects/{slug}-app1`, in the OpenCode project picker, because OpenCode opens only Git repositories and App 1 is in every business, and types `/pdlf-init`. The agent then writes every file of the business through its real path, `/mnt/c/dev/dev-{slug}`. That starts a small skill, `pdlf-init`, which tells the agent to follow this step's reference with this step's configuration. The business's slug is the App 1 repository's name without `-app1`.

The orchestrator first checks the ledger answers, then looks for unfinished work. Every run of the business is in the ledger: its entry point's row and a row for every step it has reached. A run that has not reached its end is offered to David, at the first step that is not complete. A run whose next step belongs to a phase PDLF has not yet built is reported as paused there, and waits.

When David starts new work, he chooses one of the entry points, Steps 2 to 10: a new application, an application that brings context, a feature, an update, a release, App 3 or App 5. The entry point asks its questions, checks the business is healthy when the app already exists, and writes the entry record into its own row in the ledger. For a new business it first writes the business's row. Every later step reads the entry record from there.

The orchestrator then runs the run's route, the list of its steps in order. Before each step it checks the steps it depends on are complete and every gate before it has passed. It reads the step's configuration, reference and test specification and carries the reference out. Every step opens its own row in the ledger as it starts, and ends by asking David to close out the session. When David says "continue", the next step starts.

At a gate, the step shows David the gate summary. When he says yes, the orchestrator gives him a one-line command, `pdlf-gate.sh`, which records his approval in the ledger. The orchestrator then reads the ledger to check it is there.

## Why it works this way

- **It opens in App 1.** Everything a run writes belongs to one business. Cupcake lets an agent opened in any repository of a business write anywhere in that business, so the run can reach its own business and nothing else, PDLF included.
- **It resumes, never restarts.** PDLF is proven phase by phase on the same `mb-3-cs` run. The orchestrator finds where that run stopped from the ledger alone, so David never has to remember it, and nothing already proven is done again.
- **Each step opens its row at the start.** A step that stopped part-way through, because a session ended or something failed, is then visible, and is the step the run resumes at.
- **It runs only the phases that are built.** A step that is not yet built would be carried out from old drafts. The run waits at the first such step until its phase is built.
- **The skill is only a launcher.** The steps' documents are the design. While a phase is being proven, every correction is made to those documents, and the skill never needs to change.
- **David records every gate.** A gate is the point where David commits to everything before it. If the agent could write its own approval, the gate would depend on the agent behaving. Cupcake blocks the agent from writing a gate, so a passed gate is always David's decision.
- **One run order.** The routes and the dependencies are written once, in this step's configuration, so the orchestrator and every step's own check read the same order.

## What has to happen

- David installs the `pdlf-init` skill with the command in the configuration, and again whenever its source changes.
- David opens `projects/{slug}-app1` in OpenCode before running `/pdlf-init`. For a new business, he first creates the App 1 folder, runs `git init` in it and adds its link.
- David chooses the run to continue or the entry point to take, and answers the entry's questions.
- David runs `/mb-close-out` after every step and says "continue" to go on.
- David records every gate's approval with `pdlf-gate.sh`.
