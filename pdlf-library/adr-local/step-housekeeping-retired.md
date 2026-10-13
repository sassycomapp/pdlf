---
title: "step-housekeeping-retired"
doc-id: "mb-4cb26f1b"
updated: "2026-10-13"
---
# ADR — Step Housekeeping Retired; Every Step Ends with Close-Out

**Status:** Accepted

**Date:** 2026-10-13

---

## Context

Every step must leave its work saved, committed and remembered. The build plan (section 8) settles who does each of these: the agent never commits or pushes; only David commits, with `commit-all`; new knowledge reaches GBrain only at close-out, through `/mb-close-out` and `mb-submit-memory`; and the GBrain dream cycle runs only in Sunday maintenance. Some documents still made each step do this work itself, which contradicts the build plan.

## Decision

Every step ends the same way: it explains in plain language what was done and why, shows the Step Receipt, stops, and asks David to run `/mb-close-out`. Nothing else. No step asks to commit or push, submits memory, runs the dream cycle or syncs GBrain.

A gate adds only its ceremony: Full BFT, the gate summary, David's explicit yes or no, and the gate row. The gate then ends like every other step, with the request for `/mb-close-out`.

The step's record is the ledger row, the BFT record and the Step Receipt. There is no devlog and no judgement trail.

The rule is stated in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md), and listed in [[[pdlf:pdlf-library/policy-local/pol-index|Policy Index]]](C:/pdlf/pdlf-library/policy-local/pol-INDEX.md). How memory is written is stated in [[[pdlf:pdlf-library/policy-local/pol-memory-and-knowledge|Policy: Memory and Knowledge]]](C:/pdlf/pdlf-library/policy-local/pol-memory-and-knowledge.md).

## Why

- Only David commits, so a commit happens when he has checked the work, never as a side effect of a step.
- Memory written at close-out passes through the memory governor once, with David's approval, so the same fact cannot be stored twice or in two different forms.
- One ending for every step means the agent never has to choose how a step ends.

## Consequences

- The two execution specifications and the five Phase B reference files end every step with the request for `/mb-close-out`.
- Every step designed from now on follows the same ending; no step file repeats commit or memory instructions.
