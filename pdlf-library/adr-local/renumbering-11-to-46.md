---
title: "renumbering-11-to-46"
doc-id: "mb-b9252e6c"
updated: "2026-10-20"
---
# ADR — Renumbering from 11 to 46

**Status:** Accepted (see superseding note below)

**Date:** 2026-07-10

---

## Context

The v4 step model used 36 entries numbered 0–25 with sub-steps (6a, 8a, 13a, 13b, 14a,
15a, 15b, 15c, 23a, 23b, 23c). This numbering had no room for expansion and sub-step
naming was inconsistent with the stepwise decomposition model where every entry is a
discrete skill.

## Decision

All steps are renumbered to a clean 11–46 sequence. Sub-steps become regular steps
(6a→18, 8a→21, 13a→27, etc.). Slots 1–10 are reserved for future steps that may be
inserted ahead of the existing 36. The numbering is fluid during development and may
be renumbered again later.

## Consequences

- 36 steps, numbered 11 through 46.
- All documents referencing step numbers were updated (SKILL-v4.md, skill-workflow-table.md,
    [[[pdlf:pdlf-library/templates-local/bft-checkpoint-cheatsheet-v2|BFT Checkpoint Cheatsheet v2]]](C:/pdlf/pdlf-library/templates-local/bft-checkpoint-cheatsheet-v2.md), skill-design-spec.md, policy-local files, templates).
- The installed skill at `C:\pdlf\skill\SKILL.md` and the dev source at
  `C:\dev\dev-makepdlf\skill\SKILL-v4.md` are now in sync.
- The installed file still has 3 rows of old numbers in its §0.2 reference table
  — a known discrepancy to be resolved when the installed skill is rebuilt as v5.
- Numbering is NOT locked. Files will likely be renumbered again during development.

---

## Superseding note (2026-07-13)

The final line of Consequences — "numbering is NOT locked, files will likely be
renumbered again" — is superseded. A later decision fixed canonical step numbers as
permanent identifiers: they never indicate execution order (that lives exclusively in
the mapping documents' `Execution Order` column), and new steps are added via a letter
suffix on the nearest preceding number (e.g., `35A`, `40B`) rather than renumbering
existing files. [[pdlf:obsolete/stepwise-development-process|Policy: Stepwise]] Section C records this as an explicit supersession of
its own earlier "numbering is fluid" stance. This ADR's original Decision and Context
are left unedited as the historical record of why 11–46 was chosen in the first place;
only the "will be renumbered again" expectation is retracted.
