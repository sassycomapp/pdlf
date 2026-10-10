---
title: "run-plan"
doc-id: "mb-03239097"
updated: "2026-10-10"
---
# PDLF Run Plan

**Purpose:** This file is the execution-order decision tree for the PDLF stepwise package.
While step numbers are stable identifiers (see `INDEX.md`), they do not define execution
order. This file defines which step fires next based on project state, gate outcomes,
and optional step decisions. The PDLF orchestrator loads this file to determine the next
step.

**Use:** The orchestrator consults this file after each step completes. Based on the
current step, project mode (full/test), gate outcomes, and developer decisions, it
determines the next step and loads the corresponding stepwise skill.

---

## Entry Mode

Every step always runs, for every project, regardless of whether the project is new or
existing. There is no disposition audit and no separate existing-project sequence.

Immediately after Step 11 completes, execution proceeds directly to Step 12, for both
entry modes:

```
Step 11 Complete → Step 12
```

What differs between a new and an existing project is never *whether* a step runs — only
what material a step starts from. Step 11 itself already asks whether the project is new
or existing and handles the two cases internally (repo creation and templating vs.
confirming what already exists). Step 12 does the same: new-project entry works from the
three pre-project files; existing-project entry works from the whole existing
project-library, read via GBrain. See [[[pdlf:stepwise/step-12-office-hours|Step 12: Office Hours]]](C:/pdlf/stepwise/step-12-office-hours.md) for the full mechanics.

Submitting an existing project to PDLF means redeveloping it around its canonical
concept — not auditing, maintaining, or correcting what already exists. From Step 12
onward, an existing project runs exactly the same sequence as a new one; if existing
material already satisfies what a given step needs, that step completes quickly because
there's nothing left to change, not because something decided to skip it.

---

## Phase Boundaries

Entry into the next phase requires the preceding phase's gate to pass.

| Phase | Steps | Entry Condition | Exit Gate |
|---|---|---|---|
| Phase A — Discover & Define | 11, 12, 14, 15, 16 | Init complete (Step 11) | `domain-locked` (Step 16) |
| Phase B — Design & Plan | 17–24, 26–28 | `domain-locked` passed | `concept-locked` (Step 21), `wireframes-approved` (Step 26) |
| Phase C — Scaffold & Assemble | 29–34 | `wireframes-approved` passed | `architecture-verified` (Step 34) |
| Phase D — Build & Verify | 35, 35A, 40, 40B, 36, 37, 38, 38A, 39 | `architecture-verified` passed | `build-verified` (Step 39, end of per-feature loop) |
| Phase E — Ship & Monitor | 41, 42, 42A, 43–46 | `build-verified` passed (all features) | `production-released` (Step 44), `released` (Step 46) |

Step 13 (`to-spec`) and Step 25 (`prototype`) have been removed from the pipeline. They do
not appear in any phase and have no dependency entries below.

---

## Step Dependencies

Each step requires specific preceding steps to have completed successfully. The orchestrator
checks the ledger before advancing.

| Step | Depends On (Must Be Complete) |
|---|---|
| 12 | 11 |
| 14 | 12 |
| 15 | 12, 14 |
| 16 | 15 |
| 17 | 15, 16 |
| 18 | 17 |
| 19 | 14, 15, 16, 17 |
| 20 | 12 |
| 21 | 14, 15, 16, 20 |
| 22 | 20 |
| 23 | 19, 20, 22 |
| 24 | 23 |
| 26 | 22 |
| 27 | 26 (deferred — skip unless explicitly requested) |
| 28 | 27 (deferred) |
| 29 | 22, 26, 27, 28 |
| 30 | 29 |
| 31 | 15, 16, 21, 30 |
| 32 | 31 |
| 33 | 32 |
| 34 | 15, 16, 18, 21, 30, 31, 33 |
| 35 | 19, 20, 26, 16, 17, 29, 31, 32, 34 |
| 35A | 35 (same feature cycle) |
| 40 | 35A, 16 (same feature cycle) |
| 40B | 40 — requires developer approval of Step 40's report before executing |
| 36 | 40B (same feature cycle) |
| 37 | 36 (same feature cycle) |
| 38 | 37 (same feature cycle) |
| 38A | 38 (same feature cycle) |
| 39 | 19, 38A (same feature cycle) |
| 41 | 39 (`build-verified` gate passed for every feature — not just one) |
| 42 | 41 |
| 42A | 42 |
| 43 | 42A |
| 44 | 43 |
| 45 | 44 |
| 46 | 45 |

---

## Gate Branching

At each gate step, the pipeline branches:

```
Gate Step
  ├── PASS → Continue to next phase
  └── FAIL → Stop pipeline, record blocker, do not advance
```

A failed gate does not auto-resolve. The developer must address the blocker and re-run
the gate step. A passed gate is a hard checkpoint — it cannot be silently unwound.

`build-verified` (Step 39) is evaluated once per feature cycle. The pipeline does not
advance to Step 41 until every feature has individually passed its own `build-verified`
evaluation — see "Step 35 Feature Loop" below. Every gate's procedure also runs a ledger
integrity check (no orphaned `steps`/`gates`/`isc`/`deviations` rows) before the gate
summary is presented — see [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

---

## Optional Step Routing

Steps 12 (conditional yes/no), 27, 28, and 40 (optional skill portion) require a RUN/SKIP
decision:

```
Optional Step
  ├── RUN → Execute full step procedure
  └── SKIP → Record skip in ledger, proceed to next step
```

The agent presents a recommendation with justification. The developer decides. A skipped
step still produces a Step Receipt recording the skip decision.

Step 40's RUN/SKIP decision is made once per feature cycle, not once for the whole project
— each feature entering the loop gets its own recommendation and decision.

---

## Test-Mode Branching

When the project mode is `test`, Step 20 is eligible for abbreviation:

```
Test Mode — Abbreviated Eligible Step
  ├── FULL  → Run the complete skill procedure
  ├── ABBREVIATE → Run a collapsed version, produce a minimal artifact
  └── SKIP → Record skip, use pre-existing inputs as artifact
```

Abbreviated steps write `synthesized = true` to the ledger. This tag propagates — any
downstream step consuming a synthesized artifact shows an INPUT NOTICE warning on its
receipt. A skipped step writes `status = "skipped"` with similar propagation.

Full mode projects are entirely unaffected. The abbreviation offer is never presented.

---

## Step 35 Feature Loop

Steps 35 through 39, including all lettered sub-steps, form a single loop that repeats
once per feature/package. A feature is not considered complete until it has passed
through the entire sequence below and reached `build-verified`.

```
Feature Cycle Entry (one per issue/ticket from Step 19)
  │
  ├── Step 35  — Build feature. Internal 3-level testing (pure logic →
  │              Uplink integration → manual verification), with a backup
  │              before and after the integration level.
  │
  ├── Step 35A — Testing: local-scope pip-audit (dev/test tooling only)
  │              + broader test coverage for this feature.
  │
  ├── Step 40  — Architecture scan (optional, read-only report) for this
  │              feature's code. Optional — RUN/SKIP decision per feature cycle.
  │
  ├── Step 40B — If Step 40 ran and produced findings: developer reviews
  │              and approves specific fixes. OpenCode applies only the
  │              approved fixes. Skipped entirely if Step 40 was skipped
  │              or produced no findings requiring action.
  │
  ├── Step 36  — Design review. Runs after remediation, not before —
  │              this retests the feature as it will actually ship.
  │
  ├── Step 37  — Code review. Must persist findings to
  │              step-37-findings.md, including a clean-pass statement.
  │
  ├── Step 38  — QA, cross-feature + regression. Must persist findings to
  │              step-38-findings.md, including a clean-pass statement.
  │
  ├── Step 38A — Capture Anvil's native pip-audit result for this cycle,
  │              if a server-environment rebuild occurred.
  │
  ├── Step 39  — Triage. Processes step-37/38-findings.md for this
  │              feature. build-verified gate evaluated here.
  │
  └── Gate: build-verified (evaluated for this feature only)
        ├── PASS → This feature is signed off. Record ledger row and
        │          Step Receipt for this cycle (e.g., 39.1, 39.2 ...).
        │          Return to Feature Cycle Entry for the next feature,
        │          OR — if this was the last feature — exit the loop.
        └── FAIL → Stop this feature's cycle, record blocker, do not
                   mark this feature signed off. Developer resolves,
                   re-enters the cycle at the failed step.
```

Each feature cycle produces its own ledger rows and Step Receipts for every step it
passes through, not one combined receipt for the whole loop. Do not proceed to the next
feature until the current one has reached a passed `build-verified` gate. A signed-off
feature is a known-good baseline. Step 41 is not reachable until every feature from
Step 19's ticket list has individually reached `build-verified`.

---

## Post-Completion

After Step 46 completes:
- The `released` gate is recorded.
- The ISA's Verification section is filled and Changelog updated.
- The registry is updated: `current_step: 46`, `last_gate: "released"`, `active: false`.
- GBrain is synced and embedded.
- The project is complete.
