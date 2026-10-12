---
title: "matt-pocock-skills-local-reference"
doc-id: "mb-b97bfee0"
updated: "2026-10-12"
---
# PDLF — Matt Pocock Skills Local Reference

**Purpose:** PDLF-specific integration points, artifact governance, and project paths for Matt Pocock skills within PDLF.

**Source:** Extracted from `system-description(check).md` (2026-07-12 research pass). Updated 2026-07-13 to reflect current step numbering and configuration.

**Note:** For general Matt Pocock skills reference (catalog, v1.1.0 changes, behavioral detail), see `C:\mybizz\matt-pocock-skills-source`.

---

## Layer roles

| Layer | Tool | Role |
|---|---|---|
| Orchestration | PDLF | Full project lifecycle, stage-gated |
| Workflow | GStack | Planning reviews, QA, review, ship |
| Engineering discipline | Matt Pocock skills | Domain modeling, tickets, triage, architecture |
| Memory | GBrain | Persistent knowledge base |

---

## PDLF integration points

| PDLF Step | Matt Pocock Skill | Notes |
|---|---|---|
| Step 16 | `/grill-with-docs` (using [[[pdlf:app-factory/phase-b-discover-and-define/b16-reference\|Step 16 Domain Modeling]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-reference.md) internally) | Domain glossary + ADRs, gate `domain-locked` |
| Step 19 | [[[pdlf:app-factory/phase-c-design-and-plan/c19-reference\|Step 19 to Tickets]]](C:/pdlf/app-factory/phase-c-design-and-plan/c19-reference.md) | Breaks locked plan into tracer-bullet tickets |
| Step 39 | `triage` | Processes findings from Steps 36–38, gate `build-verified` |
| Step 40 | [[[pdlf:app-factory/phase-e-build-and-verify/e40-reference\|Step 40 Improve Codebase Architecture]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40-reference.md) | Optional architecture health scan, read-only |

Previously removed skills: `to-spec` (old Step 13), `prototype` (old Step 25) — removed per the skill-use principle.

---

## Artifact governance (per local `AGENTS.md`)

| Skill | Destination |
|---|---|
| [[[pdlf:app-factory/phase-b-discover-and-define/b16-reference\|Step 16 Domain Modeling]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-reference.md), `grill-with-docs` | `CONTEXT.md` + `adr-local/` |
| [[[pdlf:app-factory/phase-c-design-and-plan/c19-reference\|Step 19 to Tickets]]](C:/pdlf/app-factory/phase-c-design-and-plan/c19-reference.md) | `.scratch/` |
| `triage` | `triage_findings` ledger table (`.scratch/` is transient input, not authoritative) |
| `setup-matt-pocock-skills` | `agents/` + AGENTS.md |
| `handoff`, [[[pdlf:app-factory/phase-e-build-and-verify/e40-reference\|Step 40 Improve Codebase Architecture]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40-reference.md) | `%TEMP%` + `matt-skills-output/` |
| `teach` | `C:\mybizz\matt-pocock-skills-source\skills\productivity\teach` |
| Others | Ask before saving |

---

## Project SLUGs

Form confirmed: `sassycomapp-{slug}-project-library` — slug before "-project-library,"
not after. Verified against `project-inventory.md`'s real GStack paths and the actual
GitHub repo (`https://github.com/sassycomapp/mb5pdlf-project-library`, local path
`C:\dev\dev-mb5pdlf\mb5pdlf-project-library`).

| Project | SLUG |
|---|---|
| mb-3-cs project-library | `sassycomapp-project-library` — **known legacy exception**, does not follow the standard form |
| mb4ecom project-library | `sassycomapp-mb4ecom-project-library` |
| mb5pdlf project-library | `sassycomapp-mb5pdlf-project-library` |
| pdlf | `sassycomapp-pdlf` |
