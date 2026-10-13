---
title: "spec-gate-procedure"
doc-id: "mb-e1c94b00"
updated: "2026-10-13"
---
# PDLF Gate Procedure

**Purpose:** This file is the single source of truth for the gate ceremony that gate steps
follow. A gate is a hard checkpoint — the developer must explicitly approve before the
pipeline continues past it. Non-gate steps do not reference this file.

**Use:** At a gate step, as part of the execution sequence in `[[spec-execution-discipline]]`, the agent
expands the step with the gate ceremony defined below. The agent does not proceed past
a gate without explicit developer approval. If approval is denied, the agent stops and
records the blocker.

---

## Gate Ceremony

In addition to the standard execution sequence, at every gate:

### 1. Full BFT Override

Full BFT applies regardless of the step's assigned level in the BFT cheatsheet. Gates
always get Full — all six questions (BONES, MUSCLE, NERVES, FAT, SKIN, HEALTH) answered.
A gate is never a Light or None BFT occasion.

### 2. Gate Summary Block

Presented to the developer in this visually distinct format:

```
██████████████████████████████████████████████
█  GATE — {gate_name}
█
█  Step: {step_number}   BFT: Full — all six passed
█
█  Proceed to next phase? (yes/no)
██████████████████████████████████████████████
```

### 3. Developer Approval

The agent does not proceed past a gate without explicit approval:
- **Yes:** Gate passes. Ledger row written with gate approval timestamp. Continue to next step.
- **No:** Gate blocked. Agent stops and records the blocker. Pipeline does not advance.

---

## The Seven Gates

Each gate, the step it follows and what it locks are recorded in that step's config (`{letter}{number}-config.md`). The gates currently sit after Steps 16, 21, 26, 34, 39, 44 and 45 with 46.

---

## After a Gate

A passed gate is a hard checkpoint. After gate approval:
- The gate's row is written to the `gates` table with timestamp and approval.
- The step's ledger row is written with `completed_at`.
- A Step Receipt is generated.
- The agent explains what was done and why, stops, and asks the developer to run `/mb-close-out`.

A gate that was passed cannot be silently unwound. Reopening a gate requires a formal
deviation request with developer authorization.
