---
title: "step-conditional-state-policy"
doc-id: "mb-5a62c5ff"
updated: "2026-10-10"
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

### Step 12 — /office-hours (conditional, NOT test-mode-eligible)

Step 12 is a simple yes/no decision gate. The developer chooses:

- **Yes:** Run [[[pdlf:stepwise/step-12-office-hours|/office-hours]]](C:/pdlf/stepwise/step-12-office-hours.md) → `status = "complete"`, `synthesized = false`.
  Design doc produced by [[[pdlf:stepwise/step-12-office-hours|/office-hours]]](C:/pdlf/stepwise/step-12-office-hours.md).
- **No:** OpenCode synthesizes a design doc from the pre-project documents →
  `status = "complete"`, `synthesized = true`. Design doc produced by OpenCode.

Step 12 always produces a design document. The `synthesized` flag indicates
whether it came from [[[pdlf:stepwise/step-12-office-hours|/office-hours]]](C:/pdlf/stepwise/step-12-office-hours.md) or from OpenCode's synthesis. There is no
`skipped` state for Step 12 — the step always completes with an artifact.

There is no abbreviation offer for Step 12. The developer either runs the full
skill or OpenCode synthesizes from the pre-project docs.

### Step 20 — /design-consultation (test-mode-eligible)

Step 20 offers abbreviation when `projects.mode = "test"`:

- **Full:** Run complete [[[pdlf:stepwise/step-20-design-consultation|/design-consultation]]](C:/pdlf/stepwise/step-20-design-consultation.md) → `status = "complete"`, `synthesized = false`
- **Abbreviated:** Run collapsed version → `status = "complete"`, `synthesized = true`
- **Skip:** Developer declines entirely → `status = "skipped"`, `synthesized = false`

In full mode, the abbreviation offer is never presented. Step 20 runs fully or
is skipped.

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
- Step 12: yes/no gate still applies (developer can decline [[[pdlf:stepwise/step-12-office-hours|/office-hours]]](C:/pdlf/stepwise/step-12-office-hours.md) and OpenCode synthesizes)
- Step 20: runs fully or is skipped (if conditional)
- The `synthesized` flag can still be set for Step 12 (OpenCode synthesis when [[[pdlf:stepwise/step-12-office-hours|/office-hours]]](C:/pdlf/stepwise/step-12-office-hours.md) declined)

---

## Resolution Note

This policy resolves todo item 5.2 (define "third state" for Step 12).

The original question: "the developer says no to [[[pdlf:stepwise/step-12-office-hours|/office-hours]]](C:/pdlf/stepwise/step-12-office-hours.md) at all (using
only the pre-project docs) — that's different from `synthesized`."

Answer: when the developer declines [[[pdlf:stepwise/step-12-office-hours|/office-hours]]](C:/pdlf/stepwise/step-12-office-hours.md), OpenCode synthesizes a
design doc from the pre-project documents. This is the `synthesized` state —
an artifact IS produced, but by OpenCode, not by the skill. Step 12 always
produces a design doc; the `synthesized` flag indicates its provenance.
