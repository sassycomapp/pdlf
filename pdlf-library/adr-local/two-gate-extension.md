---
title: "two-gate-extension"
doc-id: "mb-69dcaa24"
updated: "2026-10-11"
---
# ADR — Two-Gate Extension

**Status:** Accepted

**Date:** 2026-07-10 (gate-position detail updated 2026-07-13 — see note at end)

---

## Context

The original PDLF v2 model had five gates. Real-world project experience showed that
scope drift and architecture drift were recurring failure modes — features were added
after design was locked, and the physical Anvil build diverged from the agreed
architecture before any code was written.

## Decision

Two new hard gates were added, bringing the total to seven:
- `concept-locked` (Step 21): A full cross-document coherence audit before any wireframe
  work begins. After this gate, no new feature may be added without formal gate reopening.
- `architecture-verified` (Step 34): Confirms the physical Anvil build (data tables, UI
  forms, scaffolding) matches the locked architecture before any code-writing begins.

Additionally, `production-released` was split from the original `released` gate, giving
the production publish its own hard checkpoint.

## Consequences

- Seven gates now: `domain-locked` (Step 16), `concept-locked` (21), `wireframes-approved`
  (26), `architecture-verified` (34), `build-verified` (39), `production-released` (44),
  `released` (45+46 jointly).
- Two additional stops in the pipeline. The developer judged these worth their cost
  given prior experience of what breaks without them.
- The sanity audit procedures for both new gates live in the step files themselves:
  [[[pdlf:app-factory/phase-c-design-and-plan/21-concept-sanity-audit|Step 21 Concept Sanity Audit]]](C:/pdlf/app-factory/phase-c-design-and-plan/21-concept-sanity-audit.md) (the earlier
  `step-8a-15c-sanity-audit-procedures.md` was retired with the legacy stepwise files) and
  [[[pdlf:app-factory/phase-d-scaffold-and-assemble/34-architectural-sanity-audit|Step 34 Architectural Sanity Audit]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/34-architectural-sanity-audit.md).
- Each gate follows the expanded gate ceremony defined in [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

---

*Note (2026-07-13): `build-verified`'s position was originally Step 40. It was moved to
Step 39 by a later decision (the numbered-era ADR `build-verified-gate-moved-to-step-39.md`
is retired; the step-numbering scheme is recorded in [[[pdlf:pdlf-library/adr-local/renumbering-11-to-46|Renumbering 11 to 46]]](C:/pdlf/pdlf-library/adr-local/renumbering-11-to-46.md)) —
architecture remediation and its retest needed to complete before this gate, not before
remediation was even applied. The Consequences section above reflects the corrected
position; the original Decision text is left as written since the two-gate addition
itself is unaffected by the later move.*
