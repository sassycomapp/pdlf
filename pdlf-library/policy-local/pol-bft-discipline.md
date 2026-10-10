---
title: "pol-bft-discipline"
doc-id: "mb-f0a9a244"
updated: "2026-10-10"
---
# PDLF Policy — BFT Discipline

**Binding.** The agent must comply at every step. No exceptions without a deviation request.

---

## What

De Bono BODY Frame Thinking runs inside every PDLF step. The depth of BFT is scoped to the
step's judgment content — not applied uniformly.

**Three levels:**

| Level | Questions | When |
|---|---|---|
| **Full** | BONES, MUSCLE, NERVES, FAT, SKIN, HEALTH | Decision-heavy steps where judgment calls are made |
| **Light** | BONES + HEALTH only | Mostly mechanical steps following locked decisions |
| **None** | Nothing — skip BFT | Pure mechanical zero-judgment operations (git pull, file conversion, publish button) |

**Gate rule:** Every gate step is Full regardless of its assigned level. A gate BFT must be
exhaustive — the developer is about to approve a locked checkpoint.

**Anti-rubber-stamping:** If a required question is blank without justification, the step is
NOT done. A BFT response that is generic, copy-pasted, or unthinking is as bad as no response
at all. Each answer must be specific to the step just completed.

---

## Why

Full six-question BFT on "bump VERSION number" produces boilerplate — the exact rubber-stamping
the project's `AGENTS.md` warns against. BFT at three levels concentrates attention where
judgment lives and prevents the BFT checkpoint from becoming a checkbox ceremony.

The developer stated explicitly: "don't take the lazy route, don't rubber-stamp, don't make
silly assumptions, remain fully diligent."

---

## Where

Every step in the PDLF pipeline. The per-step level assignment is at [[[pdlf:pdlf-library/templates-local/bft-checkpoint-cheatsheet-v2|BFT Checkpoint Cheatsheet v2]]](C:/pdlf/pdlf-library/templates-local/bft-checkpoint-cheatsheet-v2.md).
The BFT questions and level definitions are at [[[pdlf:pdlf-library/specifications-local/spec-bft|Spec: BFT]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md).

**Source:** [[[pdlf:pdlf-library/specifications-local/spec-skill-design|Spec: Skill Design]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-design.md) §2.4, bft-system-derived,
[[[pdlf:pdlf-library/specifications-local/spec-bft|Spec: BFT]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md), [[[pdlf:pdlf-library/templates-local/bft-checkpoint-cheatsheet-v2|BFT Checkpoint Cheatsheet v2]]](C:/pdlf/pdlf-library/templates-local/bft-checkpoint-cheatsheet-v2.md).

---

## Step Counts (updated 2026-07-18)

The BFT-level assignment pass is complete. Current counts, from [[[pdlf:pdlf-library/templates-local/bft-checkpoint-cheatsheet-v2|BFT Checkpoint Cheatsheet v2]]](C:/pdlf/pdlf-library/templates-local/bft-checkpoint-cheatsheet-v2.md) (version 2.1):

| Level | Count |
|---|---|
| Full | 27 |
| Light | 7 |
| None | 6 |

Total: 40 steps. This reflects `to-prd` (13) and `prototype` (25) being removed, and the
four lettered sub-steps (35A, 38A, 40B, 42A) now having assigned levels. The
`build-verified` gate is at Step 39, not Step 40.
