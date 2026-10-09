---
title: "spec-gate-procedure"
doc-id: "mb-e1c94b00"
updated: "2026-10-09"
---
# PDLF Gate Procedure

**Purpose:** This file is the single source of truth for the gate ceremony that gate steps
follow. A gate is a hard checkpoint — the developer must explicitly approve before the
pipeline continues past it. Non-gate steps do not reference this file.

**Use:** At a gate step, after completing the 13-point execution sequence, the agent
expands the step with the gate ceremony defined below. The agent does not proceed past
a gate without explicit developer approval. If approval is denied, the agent stops and
records the blocker.

---

## Gate Ceremony

In addition to the standard 13-point execution sequence, at every gate:

### 1. Full BFT Override

Full BFT applies regardless of the step's assigned level in the BFT cheatsheet. Gates
always get Full — all six questions (BONES, MUSCLE, NERVES, FAT, SKIN, HEALTH) answered.
A gate is never a Light or None BFT occasion.

### 2. Full Maintenance

```
cd dev-{slug}\{slug}-project-library
git add -A && git commit -m "pdlf gate <gate_name>: <description>" && git push
```

Then invoke GStack `/sync-gbrain` against both the doc source and the code source.
Raw `gbrain sync`/`gbrain embed` commands are not used — GStack's `/sync-gbrain` was
confirmed more reliable in practice and is the standard mechanism everywhere in PDLF.

Both repositories are committed and pushed. GBrain is synced and embedded on both sources.
This ensures the gate checkpoint is captured across all persistence layers before the
developer approves forward progress.

### 3. Gate Summary Block

Presented to the developer in this visually distinct format:

```
██████████████████████████████████████████████
█  GATE — {gate_name}
█
█  Step: {step_number}   BFT: Full — all six passed
█  Maintenance: git push complete (commit {hash})
█  GBrain: synced + embedded
█
█  Proceed to next phase? (yes/no)
██████████████████████████████████████████████
```

### 4. Developer Approval

The agent does not proceed past a gate without explicit approval:
- **Yes:** Gate passes. Ledger row written with gate approval timestamp. Continue to next step.
- **No:** Gate blocked. Agent stops and records the blocker. Pipeline does not advance.

---

## The Seven Gates

| Gate | After Step | What is Locked |
|---|---|---|
| `domain-locked` | 16 | Domain model locked, PRD reviewed, ADRs written. No new terms without formal reopening. |
| `concept-locked` | 21 | Full concept coherence audit passed. Scope frozen. No new feature may be added without formally reopening this gate. |
| `wireframes-approved` | 26 | Wireframes approved, design system complete. Visual direction locked. |
| `architecture-verified` | 34 | Data tables, UI forms, and scaffolding confirmed to match the locked architecture. No code-writing begins without this gate passing. |
| `build-verified` | 39 | Build complete, architecture scan and any developer-approved remediation applied and retested, design review done, code review done, QA passed, triage complete for this feature cycle. Evaluated once per feature — the pipeline does not advance to Step 41 until every feature has individually passed this gate. Features are known-good baselines. |
| `production-released` | 44 | Staging smoke test passed, same commit promoted to Production, databases confirmed separate. App is live. |
| `released` | 45 + 46 | Production deployed, initial canary passed, LEARN complete, ISA Verification/Changelog updated. Cycle closed. |

---

## After a Gate

A passed gate is a hard checkpoint. After gate approval:
- The gate's row is written to the `gates` table with timestamp and approval.
- The step's ledger row is written with `completed_at`.
- A Step Receipt is generated.
- The two housekeeping questions are asked.
- The agent stops and reports.

A gate that was passed cannot be silently unwound. Reopening a gate requires a formal
deviation request with developer authorization.
