---
title: "e40-reference"
doc-id: "mb-e275399d"
updated: "2026-10-12"
---

## From `40-improve-codebase-architecture.md`

## Task Execution Order

1. → Decision point: Agent presents RUN/SKIP recommendation for the architecture scan,
   for this feature cycle.
2. If RUN: run Matt `improve-codebase-architecture` against the current codebase and
   CONTEXT.md/ADRs. Explore only, read-only — no code changes at this step.
3. Write the HTML report to the OS temp directory, not the repo.
4. → Handoff: if the developer selects a candidate from the report to act on, proceed to
   Step 40B for developer-approved remediation. If not, or if this step was skipped,
   proceed directly to Step 36.
5. Follow execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md).
6. Apply BFT per [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) at assigned level.

---

## Description

Independent, read-only architecture health report, run per feature cycle as an optional
step. Does not modify code and does not carry a gate of its own — the `build-verified`
gate now lives at Step 39, after remediation (if any) has been retested, not here (see
ADR-0007). Any actual code change resulting from this step's report happens only at
Step 40B, only with explicit developer approval of specific findings.

## Inputs Required

- Live codebase from Step 35 (and 35A)
- CONTEXT.md + ADRs from Step 16

## Outputs

- Interactive HTML architecture report (if run), written to OS temp directory
- Developer's selection of which findings (if any) to act on, feeding Step 40B

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 40 | Skill (optional, per feature cycle) | | Matt `improve-codebase-architecture` |

---

## Handoff to Step 40B

If findings were selected for action, proceed to Step 40B for developer-approved
remediation. Otherwise, proceed directly to Step 36.

---

## Grilling Branch Routing

If the `improve-codebase-architecture` skill's output ends with a "grill through whichever
one you pick" step, do not invoke any grilling-family skill (`grilling`, `grill-me`,
`grill-with-docs`). Instead, route that to a deviation request per
[[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md), presenting the candidate findings as
the options:

```
DEVIATION REQUEST — Step 40 (Architecture Finding Selection)

Prescribed tool: grilling-family (not imported — routing to deviation-request flow)
Status: BLOCKED
Reason: Architecture scan produced candidate findings requiring developer selection.

Options:
  A) Select finding(s) — developer specifies which to act on, proceed to Step 40B
  B) Defer — save report, revisit later
  C) Skip — no architecture remediation this cycle
     Impact: Reported findings will not be actioned in this feature cycle

Your decision? (A/B/C)
```

The agent never decides to invoke grilling. All deviations are recorded in the `deviations`
table with description, options presented, decision, and timestamp. The developer decides.

---

## Reference

Skill path: `~/.agents/skills/improve-codebase-architecture/SKILL.md`

Gate-removal rationale — why `build-verified` is no longer here: ADR-0007.

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md)

GBrain is queried automatically at substep 1. Syncing is asked at substep 10, never auto-run.
The two housekeeping questions are asked separately, every step, never combined, never auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail are the complete checkpoint.
No separate state file, devlog file, or completion report.

Skills save where designed. PDLF process artifacts go to `<project-library>/pdlf/`.
