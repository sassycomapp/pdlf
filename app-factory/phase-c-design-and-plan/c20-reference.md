---
title: "c20-reference"
doc-id: "mb-64d59065"
updated: "2026-10-12"
---

## From `20-design-consultation.md`

## Task Execution Order

1. → Decision point: If test mode, present abbreviation offer (full/abbreviate/skip)
2. Run GStack [[[pdlf:app-factory/phase-c-design-and-plan/c20-reference|/design-consultation]]](C:/pdlf/app-factory/phase-c-design-and-plan/c20-reference.md)
3. Follow execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
4. Apply BFT per [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) at assigned level (Full)

---

## Description

Builds the design system from scratch — DESIGN.md + a preview page. Eligible
for abbreviation in test mode.

## Inputs Required

- Design doc at `<project-library>/docs-local/design-doc.md` — from Step 12 (product context)
- Repo/README for product understanding
- Existing DESIGN.md if present

## Outputs

- DESIGN.md written to repo root
- Font/color HTML preview page
- Design tokens (CSS variables / JSON)

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 20 | Skill | | GStack [[[pdlf:app-factory/phase-c-design-and-plan/c20-reference\|/design-consultation]]](C:/pdlf/app-factory/phase-c-design-and-plan/c20-reference.md) |

## Reference Files

| `[[[pdlf:pdlf-library/policy-local/pol-step-conditional-state]]](C:/pdlf/pdlf-library/policy-local/pol-step-conditional-state.md)` | Steps flagged test-mode eligible |
| Standards Library | Step 20 (M3 design) |

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
