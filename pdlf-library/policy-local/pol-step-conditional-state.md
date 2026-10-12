---
title: "step-conditional-state-policy"
doc-id: "mb-5a62c5ff"
updated: "2026-10-12"
---
# PDLF Conditional Step State Policy

**Purpose:** This file is the single source of truth for how conditional steps
record their state in the ledger. It defines the states, which steps use which,
and how downstream steps are notified when an upstream step was synthesized or
skipped.

**Use:** When a step offers a yes/no decision (run or skip) or an abbreviation
offer, the orchestrator consults this file to determine the correct ledger
values and downstream propagation.

---

## The Three States

| State | `status` | `synthesized` | Meaning |
|---|---|---|---|
| Full run | `complete` | `false` | Complete skill run, no shortcut |
| Synthesized | `complete` | `true` | OpenCode synthesized output from pre-existing inputs (Step 12), OR collapsed skill version ran (Step 20 test mode) |
| Skipped | `skipped` | `false` | Developer declined; no artifact produced. Pre-existing inputs may serve as context but no new artifact is created. |

### Key Distinction

`synthesized` is NOT `skipped`:

- **Synthesized** = the skill did not run, but OpenCode produced an artifact from
  pre-existing inputs (Step 12), OR a collapsed version of the skill ran (Step 20).
  An artifact exists.
- **Skipped** = nothing ran and no artifact was produced. Pre-existing inputs
  serve as context only. No new artifact is created.

---

## Step Eligibility

Which steps are conditional, and how each behaves, is stated in that step's own build plan (currently Steps 12 and 20).

---

## Downstream Propagation

Before invoking any step, the orchestrator checks whether any upstream step in
that step's dependency chain has `synthesized = true` or `status = "skipped"`.
If so, the Step Receipt for the current step must show an INPUT NOTICE warning:

- **Synthesized:** `INPUT NOTICE: Input from Step {N} was synthesized (OpenCode synthesized from pre-existing inputs or abbreviated test-mode run), not a full skill run. Treat this step's output as provisional to the same degree.`
- **Skipped:** `INPUT NOTICE: Input from Step {N} was skipped (developer declined). No artifact was produced. Treat downstream output as provisional.`

This ensures the taint is visible at every step downstream of a shortcut, not
just at the step where the shortcut happened.

See [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) § Synthesized Flag Propagation for the
full propagation mechanism.

---

## Full Mode

In full mode (`projects.mode = "full"`):

- Abbreviation offers are never presented

---

## Resolution Note

This policy resolves todo item 5.2 (define "third state" for Step 12).

The original question: "the developer says no to [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md) at all (using
only the pre-project docs) — that's different from `synthesized`."

Answer: when the developer declines [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md), OpenCode synthesizes a
design doc from the pre-project documents. This is the `synthesized` state —
an artifact IS produced, but by OpenCode, not by the skill. Step 12 always
produces a design doc; the `synthesized` flag indicates its provenance.
