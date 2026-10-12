---
title: "pol-sequential-enforcement-and-deviation"
doc-id: "mb-bdadd132"
updated: "2026-10-12"
---
# PDLF Policy — Sequential Enforcement and Deviation

**Binding.** The agent must comply at every step. Nothing is skipped without a recorded decision.

---

## What

### Steps run in order

Every step follows the execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md). The orchestrator does not start a step until the steps it depends on are complete in the ledger ([[[pdlf:app-factory/phase-a-init/a01-build-plan|Run Plan]]](C:/pdlf/app-factory/phase-a-init/a01-build-plan.md)).

A step is complete when its expected output exists, its thinking checkpoint is answered, its ledger row is written and its Step Receipt is produced.

### Every change is approved

Every change PDLF makes needs David's approval, until David says that a particular approval is no longer needed. The agent never reduces the approvals it asks for.

### Gates

At each gate:

1. the full thinking checkpoint is answered, whatever the step's usual level;
2. the gate summary is presented in its distinct format;
3. the agent waits for David's explicit yes or no;
4. only after a yes is the gate recorded as passed, and David is asked to run `/mb-close-out`.

The agent never passes a gate without David's yes. Cupcake enforces this. A passed gate is never silently undone; reopening it is a recorded decision. The procedure is in [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

### Deviations

If the agent cannot complete a step as written, it stops and presents a deviation request:

```
DEVIATION REQUEST — Step N

Prescribed: <skill or action>
Status: BLOCKED
Reason: <specific reason, in plain language>

Options:
  A) Authorize an alternative — <what would be done instead, and what it costs>
  B) Resolve the blocker — <what is needed>
  C) Skip this step — <what is lost>

Your decision? (A/B/C)
```

The agent never chooses for David. Every deviation is recorded in the `deviations` table: what happened, the options presented, the decision and when.

A disagreement between what the agent finds in the files and what David says is true is raised at once and settled the same way.

---

## Why

Without enforced order, an agent can skip a step, deviate quietly, or do work a skill should do, and David would not see it. Ordered steps, explicit gates and recorded deviations make every decision visible and every skip deliberate.

---

## Where

Every step. Gate steps follow [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).
