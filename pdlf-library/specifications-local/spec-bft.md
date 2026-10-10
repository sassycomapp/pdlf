---
title: "spec-bft"
doc-id: "mb-5251e43f"
updated: "2026-10-10"
---
# PDLF BFT Reference

**Purpose:** This file is the single source of truth for applying de Bono's BODY Frame
Thinking (BFT) to PDLF steps. It defines the six questions, the three application levels,
and the anti-rubber-stamping rule. Every stepwise skill file references this document:
"Apply BFT per specifications-local/spec-bft.md at the step's assigned level."

**Use:** At substep 7 of the execution sequence, the agent consults this file. For Full
BFT, answer all six questions. For Light, answer BONES and HEALTH only. For None, skip.
At any gate step, BFT is Full regardless of assigned level.

**Source:** Based on *The Master Thinker's Handbook* by Edward de Bono. The core premise:
good thinking is not intelligence; good thinking is directing attention deliberately.

---

## The Six BFT Questions

### 1. BONES — Structure

What are the essential elements?

- **Big Bones (broad):** The few major structural elements — the 3-7 things that define
  the shape of this step's output.
- **Big Bones (key):** Hinge elements — if removed, the structure collapses. These are
  the things that MUST exist for the step's output to make sense.
- **Small Bones:** Supporting elements that fill out the structure.
- **Intangible Bones:** Trust, fear, suspicion, comfort — the emotional structure. Did
  the step surface anything unspoken that affects how the output will be received?

Questions: What are the 3-7 major elements? Which are foundational? Which support?

### 2. MUSCLE — Force

What gives this movement, energy, leverage?

- **Information Muscle:** How much information was needed? How hard was it to obtain?
- **Logic Muscle:** What premises did the step start from? Does the conclusion follow?
- **Emotional Muscle:** Whose feelings were involved? Which adjectives describe them?
- **Value/Belief Muscle:** Which values guided the decisions? How did they affect thinking?
- **Habit Muscle:** Which cliches or ready-made patterns were used? Were they appropriate
  or lazy?
- **Channel Muscle:** Which existing channels (tools, APIs, skills) were used? Could others
  have been used more effectively?
- **Motivation Muscle:** What was the driving force behind the step's decisions?

Question: Which muscle was dominant? Was that the right one to lead with?

### 3. NERVES — Connections

How do the parts communicate and coordinate?

- **Achieving:** Goal-to-means chain — backward planning from the desired output to the
  actions that produce it. Is the chain complete?
- **Exploring:** Associative expansion — did the step generate alternatives or only
  execute the first path found?
- **Analyzing:** Division and classification — were things correctly decomposed?
- **Organizing:** Integration and sequencing — A + B = C. Does the combined output
  form a coherent whole?

Questions: What depends on what? What sequence matters? What information must flow?
Did you accidentally mix two networks?

### 4. FAT — Waste

What is unnecessary?

- Irrelevant details that found their way into the output.
- Over-analysis — analysis that continued past the point of diminishing returns.
- Decorative complexity — things that feel intelligent but do not help.
- Redundancy — the same idea stated multiple ways.

Three-question test for each element: Was it NECESSARY? Was it RELEVANT? Was it IMPORTANT?
What was cut? What was kept and why?

### 5. SKIN — Presentation

How should this appear externally?

- **Communication:** Is the output understandable and engaging?
- **Packaging:** Is the structure correct? Conclusion-first or build-up?
- **Sequence:** Is the order right? Tree (top-down) or necklace (step-by-step)?

Communication triad: Why should they listen? Where are they at? What do you want?

### 6. HEALTH — Is it healthy?

Two questions:
- **Good in itself?** Will it work? Is it sound? What are the risks and dangers?
- **Good for this project?** Does it fit purpose, values, resources, and timeline?
- **Consequences** of running this forward in time. What happens downstream?

---

## BFT Levels

| Level | Questions | When | Step count |
|---|---|---|---|
| **Full** | All six (BONES through HEALTH) | Decision-heavy steps where judgment calls are made — architecture, scope, design, review, gate | 27 |
| **Light** | BONES + HEALTH only | Mostly mechanical steps following locked decisions. Full six-question BFT would produce boilerplate rubber-stamping | 7 |
| **None** | Nothing — skip BFT | Pure mechanical zero-judgment operations (git pull, file conversion, publish button) | 6 |

Total: 40 steps. Counts corrected 2026-07-18 to match [[[pdlf:pdlf-library/templates-local/bft-checkpoint-cheatsheet-v2|Bft Checkpoint Cheatsheet V2]]](C:/pdlf/pdlf-library/templates-local/bft-checkpoint-cheatsheet-v2.md)
v2.1, after `to-prd`/`prototype` were removed and the four lettered sub-steps (35A, 38A,
40B, 42A) received assignments.

The per-step level assignment lives at [[[pdlf:pdlf-library/templates-local/bft-checkpoint-cheatsheet-v2|Bft Checkpoint Cheatsheet V2]]](C:/pdlf/pdlf-library/templates-local/bft-checkpoint-cheatsheet-v2.md).

---

## Gate Rule

Every gate step is Full regardless of its assigned level in the cheatsheet. A gate BFT
must be exhaustive — the developer is about to approve a locked checkpoint that cannot be
unwound without formal gate reopening. A gate is never a Light or None BFT occasion.

---

## Anti-Rubber-Stamping

If a required BFT question is blank without justification, the step is NOT done. A BFT
response that is generic, copy-pasted, or unthinking is as bad as no response at all. Each
answer must be specific to the step just completed.

> "Don't take the lazy route, don't rubber-stamp, don't make silly assumptions, remain
> fully diligent." — Developer directive

A Light BFT on "bump VERSION number" is legitimate — the step is mechanical. A Full BFT
on the same step would produce the exact boilerplate the system exists to prevent. That's
the purpose of three levels: concentrate BFT attention where judgment lives.
