---
title: "isa-template-v2"
doc-id: "mb-29fc5945"
updated: "2026-10-10"
---
# ISA — Ideal State Artifact (v2)

> **What this is:** The living done-definition for a project. Created at Step 16, updated
> at the LEARN junction, and queried at the start of the next initiative. This is the north-star
> artifact that survives across all junctions.
>
> **Where this lives:** `dev-{slug}\{slug}-project-library\pdlf\isa.md` (per-project, version-controlled)
>
> **What changed in v2:** Nothing in sections 1–6, 8–11 — they stay hand-authored exactly as
> before. Only sections 7 and 12 changed: they are now generated from the `isc` table in the
> `pdlf` Postgres database rather than hand-edited. See the note at the top of each.

---

## 1. Problem

*What problem does this project solve? State it in one to three sentences.*

<!-- fill in -->

## 2. Vision

*What does the ideal end state look like?*

<!-- fill in -->

## 3. Out of Scope

*What is explicitly NOT in this initiative?*

- 
- 
- 

## 4. Principles

*What architectural and design principles govern this project?*

- 
- 

## 5. Constraints

*What hard constraints must the solution respect?*

- 
- 

## 6. Goal

*The single sentence that defines "done" for this initiative.*

<!-- fill in -->

## 7. Criteria (ISCs)

> **GENERATED — do not hand-edit this table.** This section is regenerated on request from the
> `isc` table (`pdlf` database, filtered by `project_slug`). To add or change an ISC, update the
> `isc` table, not this file directly — otherwise this file and the ledger will disagree.

| # | ISC | How to verify | Status |
|---|-----|---------------|--------|
| <!-- isc_number --> | <!-- description --> | <!-- verify_method --> | <!-- status --> |

## 8. Test Strategy

*How will the ISCs be verified?*

<!-- fill in -->

## 9. Features

*What features are in scope? Map each feature to the ISC(s) it satisfies.*

| Feature | Satisfies ISC | Notes |
|---------|---------------|-------|
| | | |

## 10. Decisions

*Key architectural and design decisions, recorded as they're made.*

| Decision | Rationale | ADR | Date |
|----------|-----------|-----|------|
| | | | |

## 11. Changelog

*Append-only log of ISA changes.*

| Date | Change | Step |
|------|--------|------|
| | ISA created | |

## 12. Verification

> **GENERATED — do not hand-edit this table.** This section is regenerated on request from the
> `isc` table, showing each ISC's current `status` and `evidence` fields. Filled progressively as
> ISCs are verified, not only at the end.

| ISC | Verdict | Evidence |
|-----|---------|----------|
| <!-- isc_number --> | <!-- status --> | <!-- evidence --> |

---

*ISA template version 2.0. Source: LifeOS ISA concept, adapted for pdlf. Sections 7 and 12
generated from the `isc` table in the `pdlf` Postgres database.*
