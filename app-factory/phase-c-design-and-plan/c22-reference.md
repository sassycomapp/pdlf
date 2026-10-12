---
title: "c22-reference"
doc-id: "mb-56ecf085"
updated: "2026-10-12"
---

## From `22-wireframe-phase-1.md`

## Task Execution Order

1. Run Claude Wireframe Skill (Magdoub) — Phase 1
2. Follow execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
3. Apply BFT per [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) at assigned level (Full)

---

## Description

Generates 5 B&W UX wireframe approaches using DESIGN.md as design context.
Builds persistent design context on first run. Skill source: Magdoub/claude-wireframe-skill.

## Inputs Required

- Step 20 DESIGN.md + design tokens
- Codebase scan (CSS/JS/templates) + screenshots on first run
- Optimization goals from user prompt

## Outputs

- the retired `wireframe/brain/design-context.md` + the retired `design-taste.md` (persistent)
- `wireframe/DDMM-{feature}/index.html` + `styles.css` (5 B&W options)

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 22 | Tool | | Claude Wireframe Skill (Magdoub) — Phase 1 |

## Reference Files

| Standards Library | Steps 22/26 (UI) |

---

## Reference

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md)

GBrain is queried automatically at substep 1. Syncing is asked at substep 10, never auto-run.
The two housekeeping questions are asked separately, every step, never combined, never auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail are the complete checkpoint.
No separate state file, devlog file, or completion report.

Skills save where designed. PDLF process artifacts go to `<project-library>/pdlf/`.
