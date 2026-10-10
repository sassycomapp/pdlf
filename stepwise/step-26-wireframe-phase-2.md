---
title: "step-26-wireframe-phase-2"
doc-id: "mb-cef0cea0"
updated: "2026-10-10"
---
## Task Execution Order

1. Run Claude Wireframe Skill (Magdoub) — Phase 2
2. → GATE: Execute gate procedure per [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md)
3. → GATE: `wireframes-approved` — developer approval required to proceed beyond Phase B
4. Follow execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
5. Apply BFT per [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) (Full — gate override)

---

## Description

Re-run of the wireframe skill (Magdoub/claude-wireframe-skill) — skips
context-collection, adds Clean and Polished color variants.

## Inputs Required

- Existing `index.html` from Step 22
- the retired `design-taste.md` + the retired `design-context.md` from Step 22

## Outputs

- `styles-opt1.css` through `styles-opt5.css` (Clean + Polished variants)
- GATE `wireframes-approved` — full BFT, gate summary, developer approval required

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 26 | Tool | **GATE** `wireframes-approved` | Claude Wireframe Skill (Magdoub) — Phase 2 |

## Gate

| Gate | After Step | What is Locked |
|---|---|---|
| `wireframes-approved` | 26 | Wireframes approved, design system complete. Visual direction locked. |

## Reference Files

| [[[pdlf:pdlf-library/templates-local/isa-template-v2\|Isa Template V2]]](C:/pdlf/pdlf-library/templates-local/isa-template-v2.md) | Steps 26, 35, 38, 46 |
| Standards Library | Steps 22/26 (UI) |

---

## Reference

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md)
For gate procedure: [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md)

GBrain is queried automatically at substep 1. Syncing is asked at substep 10, never auto-run.
The two housekeeping questions are asked separately, every step, never combined, never auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail are the complete checkpoint.
No separate state file, devlog file, or completion report.

Skills save where designed. PDLF process artifacts go to `<project-library>/pdlf/`.
