---
title: "pol-sequential-enforcement-and-deviation"
doc-id: "mb-bdadd132"
updated: "2026-10-09"
---
# PDLF Policy — Sequential Enforcement and Deviation

**Binding.** The agent must comply at every step. No exceptions without a deviation request.

---

## What

### Step execution is sequential and hard-gated

Every step follows the 13-point execution sequence defined in [[[pdlf:makepdlf-project-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md). The agent cannot
proceed to step N+1 until step N is verified complete. This is a structural constraint, not a
checklist.

A step is verified complete when: its expected output exists, its BFT checkpoint passed at
the assigned level, its ledger row is written, and its Step Receipt is generated.

### Gate procedure

At each of the seven gates, the execution sequence expands:
- Full BFT regardless of assigned level
- Complete maintenance (git push project-library + code repo, GBrain sync + embed)
- Gate summary presented in visually distinct block format
- Explicit developer approval required before proceeding — the agent does not move past a
  gate without it

### Deviation mechanism

If the agent cannot complete a step, it does not skip silently. It presents a deviation request:

```
DEVIATION REQUEST — Step N

Prescribed tool: <skill name>
Status: BLOCKED
Reason: <specific reason>

Options:
  A) Authorize deviation — <alternative action>
  B) Do not authorize — attempt to resolve the blocker
  C) Skip this step — proceed to step N+1
     Impact: <what is lost>

Your decision? (A/B/C)
```

The agent never decides to deviate. It always asks the developer with justification.

**All deviations are recorded** in the `deviations` table with the description, options
presented, decision, and timestamp.

---

## Why

The developer is a non-technical builder who relies on the agent's judgment. Without sequential
enforcement, the agent can skip steps, deviate silently, or do work that should be done by a
specialized skill. The developer catches none of this.

The Step Receipt (generated from the ledger row) is the direct answer to the "black box"
fear: every action has a contemporaneous record, not a narrative gloss written afterward.

---

## Where

Every step in the PDLF pipeline. The execution sequence is defined in [[[pdlf:makepdlf-project-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md).
The gate procedure is defined in [[[pdlf:makepdlf-project-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-gate-procedure.md). The deviation mechanism
is defined in [[[pdlf:makepdlf-project-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md).

**Source:** [[[pdlf:makepdlf-project-library/specifications-local/spec-skill-design|Spec: Skill Design]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-skill-design.md) §5, [[[pdlf:makepdlf-project-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md),
[[[pdlf:makepdlf-project-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-gate-procedure.md).
