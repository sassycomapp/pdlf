---
title: "orchestrator-agent-explainer"
updated: "2026-10-11"
---
# PDLF — The Orchestrator (Step 1)

## What it is

The orchestrator is the agent that carries an application through PDLF, from the first question to release. It is Step 1, and its module is `01-module`. It is not a step of the pipeline in the same sense as Steps 11 to 46: it is what runs them. A skill runs once and finishes; the orchestrator stays in charge until the build is done.

The orchestrator never runs on its own. It is David's tool. It stops for David at every point where a real decision belongs to him.

## Why it exists

**For David.** David cannot personally verify the agent's code. Someone has to hold the discipline so that he does not have to. The orchestrator checks, verifies, stops and asks, so that David's trust rests on structure rather than hope.

**For the steps.** Every step repeats the same pattern. If each step file carried its own copy, the copies would drift and one would eventually skip something. The orchestrator owns that pattern once. Step files say *what* a step does; the orchestrator enforces *how* every step is carried out, identically.

## What it does

- **Establishes the entry point.** It asks David what kind of work this is (a new application, a new feature, an update, returning to another app of a five-app set) and from his answers chooses where to begin and which modules to run.
- **Runs the modules in order.** It follows [[[pdlf:pdlf-library/docs-local/orchestrator-run-plan|Run Plan]]](C:/pdlf/pdlf-library/docs-local/orchestrator-run-plan.md) and checks the ledger before every step; it never decides the order itself and never skips a step.
- **Owns the handoffs.** It passes the full text of earlier outputs into each skill, captures where each output was saved, confirms it exists, records it in the ledger and writes the copy to `output/`. A missing output stops the step with a deviation ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md)).
- **Applies the rules.** It reads a skill's own file before invoking it; uses the library's skill for every task a skill covers; runs each step's thinking checkpoint; carries out the gate procedure; and handles every deviation by setting out the options and letting David decide.
- **Explains and stops.** After every step it explains in plain language what was done and why, presents the Step Receipt, and waits.
- **Asks for close-out.** At the end of every step it asks David to run `/mb-close-out`. It never runs close-out itself, and it never commits or pushes.

Only the orchestrator, carrying out a PDLF step, writes to the ledger.

## Status

This document defines the orchestrator's role. Its executable form does not exist yet: `app-factory/phase-a-init/01-orchestrator.md` and `app-factory/phase-a-init/01-module.md` are placeholders. How the orchestrator is configured in OpenCode (including PDLF's own `opencode.json`) is decided when Step 1 is designed, in steps work.
