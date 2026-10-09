---
title: "bft-checkpoint-cheatsheet-v2"
doc-id: "mb-a25e8e8d"
updated: "2026-10-09"
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

### Phase A — Discover & Define (Steps 11–16)

| Step | Name | Type | BFT | Rationale |
|---|---|---|---|---|
| 11 | Init | OpenCode | **Full** | Creates project structure, ledger, registry entry — architectural foundation decisions |
| 12 | /office-hours | Skill (conditional) | **Full** | Six-question product interview shapes everything that follows |
| 14 | /plan-ceo-review | Skill | **Full** | Scope and ambition review — strategic decisions |
| 15 | /plan-eng-review | Skill | **Full** | Architecture, data flow, edge cases — technical decisions |
| 16 | /grill-with-docs (domain-modeling) | Skill + GATE | **Full** | Domain glossary + ADRs lock the data model. GATE `domain-locked` — full BFT mandatory |

### Phase B — Design & Plan (Steps 17–28)

| Step | Name | Type | BFT | Rationale |
|---|---|---|---|---|
| 17 | Create Anvil data tables | Manual | **Light** | Schema is already locked by ADRs from step 16. Build follows blueprint. |
| 18 | Pull to local | Manual | **None** | Pure mechanical `git pull`. Zero judgment. |
| 19 | to-tickets | Skill | **Full** | Decomposing locked plan into dependency-ordered tracer-bullet tickets — decomposition decisions |
| 20 | /design-consultation | Skill | **Full** | Creates full design system — aesthetic, colour, typography, spacing, motion decisions |
| 21 | Concept sanity audit | Gate (OpenCode) | **Full** | GATE `concept-locked`. Cross-references plan, CEO, Eng, domain model, DESIGN.md for contradictions. Scope freeze. |
| 22 | wireframe Phase 1 | Tool | **Full** | Generates 5 UX approaches — design direction decisions |
| 23 | /plan-design-review | Skill | **Full** | Rates design dimensions 0–10, identifies gaps — design review decisions |
| 24 | /plan-devex-review | Skill | **Full** | API/CLI/SDK friction analysis — DX strategy decisions |
| 26 | wireframe Phase 2 | Tool + GATE | **Full** | Final polished colour variants. GATE `wireframes-approved` — full BFT mandatory |
| 27 | Screen Production | OpenCode | **Full** | Screen HTML from wireframes — visual fidelity decisions, two-stage compliance check |
| 28 | Screen → PNG | External tool | **None** | Pure mechanical HTML-to-PNG conversion. Zero judgment. |

### Phase C — Scaffold & Assemble (Steps 29–34)

| Step | Name | Type | BFT | Rationale |
|---|---|---|---|---|
| 29 | Build UI forms (Anvil IDE) | Manual | **Light** | Anvil AI builds UI from approved screens. Design locked at step 21/26. Developer guides, not designs. |
| 30 | Pull to local | Manual | **None** | Pure mechanical `git pull`. Zero judgment. |
| 31 | Scaffold planning | OpenCode | **Full** | Plans module/function structure — structural architecture decisions |
| 32 | Physical scaffold build | Manual | **Light** | Creates empty stubs following step 31's plan. Implementation, not design. |
| 33 | Pull to local | Manual | **None** | Pure mechanical `git pull`. Zero judgment. |
| 34 | Architectural sanity audit | Gate (OpenCode) | **Full** | GATE `architecture-verified`. Confirms physical Anvil build matches locked architecture. |

### Phase D — Build & Verify (Steps 35–40)

| Step | Name | Type | BFT | Rationale |
|---|---|---|---|---|
| 35.N | Build feature N | Agent loop (each issue) | **Full** | Writes production code — every feature cycle has logic, integration, and verification decisions |
| 35A | Testing (local pip-audit + broader) | OpenCode | **Light** | Dev/test-tooling dependency scan + coverage — mechanical execution of a locked test plan, not a design decision |
| 40 | improve-codebase-architecture | Skill (optional, per feature cycle) | **Light** | Read-only report, no code touched, no gate here (moved to 39 — see [[[pdlf:makepdlf-project-library/adr-local/two-gate-extension]]](C:/pdlf/makepdlf-project-library/adr-local/two-gate-extension.md)). Optional recommendation, not a judgment-heavy step in itself. |
| 40B | Remediation | OpenCode (conditional) | **Light** | Applies only developer-approved fixes from Step 40 — scoped execution, not open design |
| 36 | /design-review | Skill | **Full** | Live-site visual audit, post-remediation retest — design quality decisions |
| 37 | /review | Skill | **Full** | Pre-landing code review — structural quality decisions |
| 38 | /qa | Skill | **Full** | Systematic QA testing + bug fixing — quality and regression decisions |
| 38A | Dependency scan confirm | OpenCode (per feature cycle) | **None** | Records Anvil's own native pip-audit result — capture only, no judgment |
| 39 | triage | Skill + GATE | **Full** | Labels, comments, issue-tracker updates from Steps 37–38 findings. GATE `build-verified` fires here (moved from Step 40 — [[[pdlf:makepdlf-project-library/adr-local/two-gate-extension]]](C:/pdlf/makepdlf-project-library/adr-local/two-gate-extension.md)) — full BFT mandatory regardless of the table's usual Light assignment for triage-type work. |

### Phase E — Ship & Monitor (Steps 41–46)

| Step | Name | Type | BFT | Rationale |
|---|---|---|---|---|
| 41 | /ship (scope narrowed) | Skill | **Light** | Version bump, CHANGELOG, commit, push. Mostly mechanical but CHANGELOG writing has judgment. |
| 42 | Publish to Staging | Manual | **None** | Click "Publish" in Anvil IDE. Zero judgment. |
| 42A | Staging integration/E2E | Skill/OpenCode | **Light** | Full integration/E2E suite against staging — executes a locked test plan, not a design decision |
| 43 | /qa or /canary at Staging | Skill | **Full** | Smoke test against live Staging — verification decisions before production promotion |
| 44 | Promote to Production | Manual + GATE | **Full** | GATE `production-released`. Commits the app to real users. Full BFT mandatory. |
| 45 | /canary at Production | Skill | **Full** | Post-deploy monitoring loop — production health decisions |
| 46 | LEARN junction | OpenCode + GATE | **Full** | Retrospective, learnings, ISA update. GATE `released` (jointly with 45). Full BFT — last checkpoint of the cycle. |

---

## Summary

| BFT Level | Count | Steps |
|---|---|---|
| Full | 27 | 11, 12, 14–16, 19–24, 26, 27, 35.N, 36–39, 43, 44, 45, 46 |
| Light | 7 | 17, 29, 32, 35A, 40, 40B, 41, 42A |
| None | 6 | 18, 28, 30, 33, 38A, 42 |

**Gates (always Full regardless of table):** 16 (`domain-locked`), 21 (`concept-locked`),
26 (`wireframes-approved`), 34 (`architecture-verified`), 39 (`build-verified` — moved
from Step 40, [[[pdlf:makepdlf-project-library/adr-local/two-gate-extension]]](C:/pdlf/makepdlf-project-library/adr-local/two-gate-extension.md)), 44 (`production-released`), 45+46 (`released`). All seven are
already marked Full above.

---

*BFT checkpoint cheat-sheet version 2.1. Updated 2026-07-18: removed Step 13 (`to-prd`,
deleted) and Step 25 (`prototype`, retired); corrected Step 19 name (`to-tickets`, not
`to-issues`); corrected `build-verified` gate location to Step 39 (was shown at Step 40 —
[[[pdlf:makepdlf-project-library/adr-local/two-gate-extension]]](C:/pdlf/makepdlf-project-library/adr-local/two-gate-extension.md)); added the 4 previously-unassigned lettered sub-steps (35A, 38A, 40B, 42A).
Step count corrected from 28/6/5 (39 total) to 27/7/6 (40 total, reflecting the 4 added
steps net of the 2 removed). Source: de Bono Master Thinker's Handbook (summarised at
bft-system-derived). Step list cross-checked against the current
stepwise files, not SKILL-v4.md (obsolete).*
