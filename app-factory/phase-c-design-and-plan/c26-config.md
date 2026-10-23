---
title: "c26-config"
doc-id: "mb-b69a9094"
updated: "2026-10-23"
---

## From `step-mapping.md`: this step's rows

### Phase B — Design & Plan

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 26 | `[[step-26-wireframe-phase-2]]` | Tool + GATE | Wireframe skill (Magdoub) — Clean/Polished | `wireframes-approved` |

### Phase B — Design & Plan: phase notes

Exit gates: `concept-locked` (Step 21), `wireframes-approved` (Step 26). For entry
condition and dependencies, see Run Plan.

### Gate Summary

`build-verified` sits at Step 39 (triage), not Step 40 — architecture remediation (40,
40B) must complete and be retested (36, 37, 38) before the gate is evaluated, not after
(ADR: two-gate-extension). Note this table lists gates in phase order for readability;
it is not a sequence claim — see Run Plan for the loop's actual internal order.

| Gate | After Step |
|---|---|
| `wireframes-approved` | 26 |

## From `bft-checkpoint-cheatsheet-v2.md`: BFT level

### Phase C — Design & Plan (Steps 17–28)

| Step | Name | Type | BFT | Rationale |
|---|---|---|---|---|
| 26 | wireframe Phase 2 | Tool + GATE | **Full** | Final polished colour variants. GATE `wireframes-approved` — full BFT mandatory |

## From `spec-gate-procedure.md`: gate

| Gate | After Step | What is Locked |
|---|---|---|
| `wireframes-approved` | 26 | Wireframes approved, design system complete. Visual direction locked. |
