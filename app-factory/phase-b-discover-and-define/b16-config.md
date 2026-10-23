---
title: "b16-config"
doc-id: "mb-e2e6e760"
updated: "2026-10-23"
---

## From `step-mapping.md`: this step's rows

### Phase A — Discover & Define

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 16 | `[[step-16-domain-modeling]]` | Skill + GATE | `/grill-with-docs` (using /domain-modeling) | `domain-locked` |

### Phase A — Discover & Define: phase notes

Exit gate: `domain-locked` (Step 16). For entry condition and dependencies, see Run Plan.

### Gate Summary

`build-verified` sits at Step 39 (triage), not Step 40 — architecture remediation (40,
40B) must complete and be retested (36, 37, 38) before the gate is evaluated, not after
(ADR: two-gate-extension). Note this table lists gates in phase order for readability;
it is not a sequence claim — see Run Plan for the loop's actual internal order.

| Gate | After Step |
|---|---|
| `domain-locked` | 16 |

## From `bft-checkpoint-cheatsheet-v2.md`: BFT level

### Phase B — Discover & Define (Steps 11–16)

| Step | Name | Type | BFT | Rationale |
|---|---|---|---|---|
| 16 | /grill-with-docs (domain-modeling) | Skill + GATE | **Full** | Domain glossary + ADRs lock the data model. GATE `domain-locked` — full BFT mandatory |

## From `spec-gate-procedure.md`: gate

| Gate | After Step | What is Locked |
|---|---|---|
| `domain-locked` | 16 | Domain model locked, PRD reviewed, ADRs written. No new terms without formal reopening. |

## From `matt-pocock-skills-local-reference.md`: skill used

| PDLF Step | Matt Pocock Skill | Notes |
|---|---|---|
| Step 16 | `/grill-with-docs` (using [[[pdlf:app-factory/phase-b-discover-and-define/b16-reference\|Step 16 Domain Modeling]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-reference.md) internally) | Domain glossary + ADRs, gate `domain-locked` |

## From `matt-pocock-skills-pdlf-compliance.md`: skill in scope

| Skill | Used at | Type | Wrapper or Fat |
|---|---|---|---|
| [[[pdlf:app-factory/phase-b-discover-and-define/b16-reference\|Step 16 Domain Modeling]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-reference.md) | Step 16 (invoked via `/grill-with-docs`) | Model-invoked | Fat, self-contained |
