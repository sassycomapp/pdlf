---
title: "spec-gate-procedure"
doc-id: "mb-e1c94b00"
updated: "2026-10-24"
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

| Gate | At step | What it locks |
|---|---|---|
| `domain-locked` | 16 | The domain model: the glossary, its decisions and the data design they agree with; and with them every output of Phase B, which Phase C builds on |
| `concept-locked` | 21 | The concept, after a cross-document coherence audit; no feature is added after it without the gate being reopened |
| `wireframes-approved` | 26 | The wireframes and screens |
| `architecture-verified` | 34 | The physical Anvil build (Data Tables, forms, scaffolding) matches the locked architecture, before any code is written |
| `build-verified` | 39 | The feature, after remediation and its retest |
| `production-released` | 44 | The production release |
| `released` | 45 and 46 jointly | The release in service |

Each gate's detail is recorded in its step's config (`{letter}{number}-config.md`).

Why these gates: scope drift and architecture drift are the recurring failures. `concept-locked` stops features entering after design is settled, and `architecture-verified` stops the built Anvil app diverging from the agreed architecture before code is written.

---

## After a Gate

A passed gate is a hard checkpoint. After gate approval:
- The gate's row is written to the `gates` table with timestamp and approval.
- The step's ledger row is written with `completed_at`.
- A Step Receipt is generated.
- The agent explains what was done and why, stops, and asks the developer to run `/mb-close-out`.

A gate that was passed cannot be silently unwound. Reopening a gate requires a formal
deviation request with developer authorization.
