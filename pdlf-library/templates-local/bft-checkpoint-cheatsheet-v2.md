---
title: "bft-checkpoint-cheatsheet-v2"
doc-id: "mb-a25e8e8d"
updated: "2026-10-12"
---
# BFT Checkpoint — Cheat Sheet v2

> **What this is:** Reference for applying de Bono's BODY Frame Thinking as a checkpoint at
> every PDLF step. The agent must answer the assigned questions before a step is "done."
> **Source:** de Bono's Master Thinker's Handbook — summarised in
> `docs-local/pre-pdlf/BFT system derived.md`. Adapted for PDLF v4's 36-step model.
>
> **Rule:** BFT runs inside every step, not as a separate step. If a required question is blank
> without justification, the step is NOT done.

---

## The Six Questions

### 1. BONES — Structure

What are the essential elements?

- **Big bones (broad):** The few major structural elements
- **Big bones (key):** Hinge elements — if removed, the structure collapses
- **Small bones:** Supporting elements
- **Intangible bones:** Trust, fear, suspicion, comfort — the emotional structure

Questions: What are the 3–7 major elements? Which are foundational? Which support?

### 2. MUSCLE — Force

What gives this movement, energy, leverage?

- Information muscle (how much? how hard?)
- Logic muscle (starting premises? does it follow?)
- Emotional muscle (whose feelings? which adjectives?)
- Value/Belief muscle (which values? how do they affect thinking?)
- Habit muscle (which clichés/ready-mades? adversarial or welcomed?)
- Channel muscle (which existing channels? can we use them?)
- Motivation muscle (what is the driving force?)

Question: Which muscle was dominant? Was that the right one to lead with?

### 3. NERVES — Connections

How do the parts communicate and coordinate?

- **Achieving:** Goal → means, backward planning
- **Exploring:** Associative expansion, ideation
- **Analyzing:** Division/classification, decomposition
- **Organizing:** A+B=C, integration, sequencing

Questions: What depends on what? What sequence matters? What information must flow?
Did you accidentally mix two networks? (Common: decomposition + integration in one diagram.)

### 4. FAT — Waste

What is unnecessary?

- Irrelevant details
- Over-analysis
- Decorative complexity
- Things that feel intelligent but do not help

Three-question test: Was each element NECESSARY? RELEVANT? IMPORTANT?
What was cut? What was kept and why?

### 5. SKIN — Presentation

How should this appear externally?

- Communication: understandable and engaging?
- Packaging: correct structure (up-front conclusion vs build-up)?
- Sequence: tree or necklace?

Communication triad: Why should they listen? Where are they at? What do you want?

### 6. HEALTH — Is it healthy?

Two questions:
- **Good in itself?** Will it work? Is it sound? Risks and dangers?
- **Good for this project?** Fits purpose, values, resources, timeline?
- **Consequences** of running this forward in time.

---

## BFT Levels — When Full, Light, or None

| Level | Questions | When |
|---|---|---|
| **Full** | All six (BONES through HEALTH) | The step makes substantial judgment calls — architecture, scope, design, review, gate. Full BFT prevents unexamined decisions from accumulating. |
| **Light** | BONES + HEALTH only | The step is mostly mechanical following locked decisions, but still produces an artifact worth reflecting on. Full six-question BFT would produce boilerplate rubber-stamping. |
| **None** | Nothing (skip BFT) | Purely mechanical steps with zero judgment content (git pull, file conversion, publish button). Any BFT here IS the rubber-stamping the AGENTS.md warns against. |

**Gate rule:** Every gate step is Full regardless of its Level column below. A gate's BFT must be exhaustive — the developer is about to approve a locked checkpoint that cannot be unwound without formal reopening.

---

## Step → BFT Level Mapping

Each step's BFT level, with its reason, is recorded in that step's config (`{letter}{number}-config.md`).

---

## Summary

| BFT Level | Count | Steps |
|---|---|---|
| Full | 27 | 11, 12, 14–16, 19–24, 26, 27, 35.N, 36–39, 43, 44, 45, 46 |
| Light | 7 | 17, 29, 32, 35A, 40, 40B, 41, 42A |
| None | 6 | 18, 28, 30, 33, 38A, 42 |

**Gates (always Full regardless of table):** 16 (`domain-locked`), 21 (`concept-locked`),
26 (`wireframes-approved`), 34 (`architecture-verified`), 39 (`build-verified` — moved
from Step 40, [[[pdlf:pdlf-library/adr-local/two-gate-extension]]](C:/pdlf/pdlf-library/adr-local/two-gate-extension.md)), 44 (`production-released`), 45+46 (`released`). All seven are
already marked Full above.

---

*BFT checkpoint cheat-sheet version 2.1. Updated 2026-07-18: removed Step 13 (`to-prd`,
deleted) and Step 25 (`prototype`, retired); corrected Step 19 name (`to-tickets`, not
`to-issues`); corrected `build-verified` gate location to Step 39 (was shown at Step 40 —
[[[pdlf:pdlf-library/adr-local/two-gate-extension]]](C:/pdlf/pdlf-library/adr-local/two-gate-extension.md)); added the 4 previously-unassigned lettered sub-steps (35A, 38A, 40B, 42A).
Step count corrected from 28/6/5 (39 total) to 27/7/6 (40 total, reflecting the 4 added
steps net of the 2 removed). Source: de Bono Master Thinker's Handbook (summarised at
bft-system-derived). Step list cross-checked against the current
step files, not SKILL-v4.md (obsolete).*
