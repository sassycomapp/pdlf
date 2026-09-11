---
document: "PDLF — The Orchestrator Agent (Step 1)"
doc-id: pdlf-expl-orchestrator-agent
state: Live
date-created: 2026-09-11
---

# PDLF — The Orchestrator Agent (Step 1)

*What the orchestrator agent is, which is Step 1, and what its function is,
how it works, and why it exists.*

---

## 1. What it is

The orchestrator is the running agent that carries a project through the
entire PDLF pipeline, one step at a time, from first contact to release. It
is Step 1 — not a pipeline step in the same sense as Steps 11–46, but the
thing that makes all of them run. It is deliberately **not** a run-once
skill: a skill runs, produces its output, and is finished. The orchestrator
never finishes until the project does. It is the standing authority that
executes every step, administers every standard, and stops for the developer
at every point where a real decision belongs to a human.

## 2. Why it exists

Two reasons, one practical and one structural.

**Practical:** the developer is non-technical and cannot personally verify
the agent's work. Someone has to hold the discipline so the developer does
not have to. That someone is the orchestrator — it checks, it verifies, it
stops, it asks. It is the mechanism that makes the developer's trust
structural rather than hopeful.

**Structural:** every pipeline step repeats the same skeleton — query
memory, assemble inputs, invoke or execute, capture the output, verify it
exists, record it, report, stop and wait. Today that skeleton exists only as
duplicated text inside each individual step file. The orchestrator is the
single owner of that skeleton. The step files define **what** each step
does; the orchestrator enforces **how** every step is executed — identically,
without exception, with no step able to skip its own discipline.

## 3. What it does

- **Runs every step in order**, per the dependency table — never deciding
  sequence itself, never skipping.
- **Owns the handoff contract:** pastes the full text of prior artifacts into
  each skill invocation, captures the output path the skill reports, verifies
  the artifact exists on disk, records the location in the ledger
  (`artifact_path`), makes the stable and safety-net copies. An expected
  artifact that is missing is a STOP with a formal deviation request — never
  a silent proceed (per `pdlf-spec-artifact-handover.md`).
- **Administers the standards:** reads a skill's own definition before
  invoking it — never trusting a name; runs the BFT checkpoint at the level
  the step assigns (Full at every gate, no exceptions); executes the gate
  ceremony; enforces the deviation mechanism (three options, developer
  decides, every outcome recorded).
- **Asks, never assumes:** the two end-of-step housekeeping questions,
  separately, every step, never combined, never run automatically. The
  documentation skills and the heavier maintenance runs are asked about at
  their proper checkpoints rather than after every step — the exact schedule
  is defined with the closeout process while it is developed in the makePDLF
  environment.
- **Stops and waits** at the end of every step, presenting the Step Receipt
  and waiting for the developer's "continue." It never advances on its own.

## 4. How it works

The orchestrator reads each step file as that step's own authority. The step
file defines the step's procedure, inputs, outputs, and handoffs; the
orchestrator supplies the uniform execution machinery around it: the opening
GBrain query (read-only, every step), the routing (skill invocation, manual
action, optional decision, or gate), the verification, the ledger write, the
receipt, and the stop. The ledger is the memory between steps and between
sessions; the receipts are the developer-facing readout; and only the
orchestrator, operating through a real PDLF step, ever writes to the ledger.

## 5. Status — defined, not yet built

This document defines the orchestrator's role and behavior. Its executable
form does not exist yet: Step 1's file in the makePDLF environment is
currently an empty placeholder, and the machinery that will run this role is
app-factory Module 1, to be produced when makePDLF builds Step 1. The
implementation shape (how the standing agent is configured and wired in
OpenCode) is a design decision to be made at that build — informed by this
explainer, the handover specification, and the built steps it will run.

---

*End of pdlf-expl-orchestrator-agent*