---
title: "devlog-index-template"
doc-id: "mb-dd9be8c1"
updated: "2026-10-10"
---
# devlog-index.md — PDLF Devlog Index

> **What this is:** A reverse-chronological list of every Step Receipt produced for this project.
> This is the human-browsable index into the full PDLF history — one line per step, newest at
> the top, linking to that step's full receipt file.
>
> **Where this lives:** `dev-{slug}\{slug}-project-library\pdlf\devlog-index.md`
>
> **Source of truth:** Generated from the `steps` table in the `pdlf` Postgres database, filtered
> by `project_slug`. This file is a **generated view** — do not hand-edit entries. If a step's
> details look wrong here, the fix is in the ledger row, not this file.
>
> **Write discipline:** Regenerated (prepend new entry) after every step's receipt is written.
> Not append-only by hand — the agent writes the new top line as part of Step Execution Discipline
> (checkpoint writing), from the same insert that produced the Step Receipt.

---

## Scaffold initialization

If this file does not exist when first needed, create it with only the following header, then
proceed. This is a one-time structural creation, not a content decision.

```
# Devlog Index — <project_name> (<slug>)
Reverse-chronological list of PDLF step receipts. Newest at top.
```

---

## Entry format

Each line:

```
- **Step {step_number}** ({date}) — {skill_family}/{skill_name or "Manual"} — {status}{gate_marker} — [receipt](./step-{step_number}-receipt.md)
```

Where `{gate_marker}` is ` — GATE: {gate_name} ({passed/pending})` if this step is a gate, and
omitted entirely otherwise.

---

## Worked example

```
# Devlog Index — Mybizz 5 (mb5pdlf)
Reverse-chronological list of PDLF step receipts. Newest at top.

- **Step 17** (2026-07-04) — Manual/Anvil data tables — complete — [receipt](./step-17-receipt.md)
- **Step 16** (2026-07-04) — matt-skills/domain-modeling — complete — GATE: domain-locked (passed) — [receipt](./step-16-receipt.md)
- **Step 15** (2026-07-04) — gstack/plan-eng-review — complete — [receipt](./step-15-receipt.md)
- **Step 14** (2026-07-03) — gstack/plan-ceo-review — complete — [receipt](./step-14-receipt.md)
- **Step 12** (2026-07-03) — gstack/office-hours — complete — [receipt](./step-12-receipt.md)
```

---

*devlog-index.md template version 1.0. Source: `steps` table, `pdlf` Postgres database.
Location: `dev-{slug}\{slug}-project-library\pdlf\devlog-index.md`.*
