---
title: "judgement-trail-template"
doc-id: "mb-c98dafec"
updated: "2026-10-10"
---
# judgement-trail.md — PDLF Judgement Trail

> **What this is:** A reverse-chronological record of every point where a human judgment call was
> made during this project — deviations approved, optional steps decided, and gates passed. This
> is the answer to "what did the developer actually decide, and when" without having to re-read
> every Step Receipt in full.
>
> **Where this lives:** `dev-{slug}\{slug}-project-library\pdlf\judgement-trail.md`
>
> **Source of truth:** Generated from the `deviations`, `steps` (where `step_type = 'optional'`),
> and `gates` tables in the `pdlf` Postgres database, filtered by `project_slug`. This file is a
> **generated view** — do not hand-edit entries.
>
> **Write discipline:** A new entry is appended (prepended, since this is reverse-chronological)
> at the moment the judgment is made — a deviation decided, an optional step run/skipped, or a
> gate approved — not reconstructed afterward from memory or transcript.

---

## Scaffold initialization

If this file does not exist when first needed, create it with only the following header, then
proceed. This is a one-time structural creation, not a content decision.

```
# Judgement Trail — <project_name> (<slug>)
Flagged issues, developer decisions, and approved deviations, extracted from the ledger as they occur. Newest at top.
```

---

## Entry formats

**Deviation:**
```
- **[DEVIATION]** Step {step_number} ({date}) — {description} — Options: {options_presented} — Decision: {decision}
```

**Optional step decision:**
```
- **[OPTIONAL]** Step {step_number} ({date}) — {skill_name} — Recommendation: {recommendation} — Decision: {run/skip}
```

**Gate approval:**
```
- **[GATE]** {gate_name} after Step {step_number} ({date}) — Passed: {yes/no} — Notes: {notes}
```

---

## Worked example

```
# Judgement Trail — Mybizz 5 (mb5pdlf)
Flagged issues, developer decisions, and approved deviations, extracted from the ledger as they occur. Newest at top.

- **[GATE]** domain-locked after Step 16 (2026-07-04) — Passed: yes — Notes: ADRs reviewed, terms consistent with existing CONTEXT.md
- **[OPTIONAL]** Step 40 (2026-07-04) — improve-codebase-architecture — Recommendation: skip (no architecture concerns for this feature) — Decision: skip
- **[DEVIATION]** Step 22 (2026-07-03) — wireframe skill returned only 3 of 5 requested B&W options — Options: A) proceed with 3, B) retry the skill, C) skip step — Decision: A, proceed with 3
```

---

*judgement-trail.md template version 1.0. Source: `deviations`, `steps`, `gates` tables, `pdlf`
Postgres database. Location: `dev-{slug}\{slug}-project-library\pdlf\judgement-trail.md`.*
