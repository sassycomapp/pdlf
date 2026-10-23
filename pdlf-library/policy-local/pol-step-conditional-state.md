---
title: "step-conditional-state-policy"
doc-id: "mb-5a62c5ff"
updated: "2026-10-23"
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

A step whose input came from a synthesized or skipped step shows an INPUT NOTICE on its Step Receipt, so the shortcut stays visible at every later step. The mechanism and the notice wording are in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md), Synthesized Flag Propagation.

---

## Full Mode

In full mode (`projects.mode = "full"`):

- Abbreviation offers are never presented
