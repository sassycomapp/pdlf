---
title: "instructions"
doc-id: "mb-abbce0c3"
updated: "2026-10-09"
---
# Instructions

Agent instructions for working within the PDLF development workspace (`C:\dev\dev-makepdlf\`).

## Agent roles

PDLF is operated by two agent roles:

- **Plan** — reads, analyzes, plans. Never writes.
- **Build** — writes with user approval. Invokes skills as prescribed.

Both are governed by the global AGENTS.md (user-level, in `~/.config/opencode/AGENTS.md`) and the local ``~/.config/opencode/AGENTS.md`` in this repo.

## Before starting any task

1. Read AGENTS.md (global + local) and `README.md`.
2. Check [[[pdlf:makepdlf-project-library/docs-local/docmap|Docmap]]](C:/pdlf/makepdlf-project-library/docs-local/docmap.md) for file locations.
3. Check `adr-local/` for relevant architectural decisions.
4. Check `policy-local/` for binding policies that may apply.
5. If the task involves testing PDLF itself or an Anvil app PDLF builds, check
   [[[pdlf:makepdlf-project-library/checklists-local/chk-pdlf-self-test|PDLF Self-Test Checklist]]](C:/pdlf/makepdlf-project-library/checklists-local/chk-pdlf-self-test.md) and
   the retired `C:\dev\project-library-global\checklists-global\chk-anvil-app-testing.md` respectively.

## Skill invocation

PDLF invokes skills from three families:

| Family | Examples | When |
|---|---|---|
| Matt Pocock | triage, domain-modeling (invoked via `/grill-with-docs`, not directly), to-tickets, handoff, implement, diagnosing-bugs, teach, grill-me, grill-with-docs, grilling | Domain work, issue management, debugging, refactoring |
| GStack | plan-ceo-review, plan-eng-review, plan-design-review, plan-devex-review, design-shotgun, design-html, design-review, qa, investigate, browse, ship, retro, health | Planning, design, QA, deployment, retrospectives |
| PDLF (custom) | pdlf (orchestrator), stepwise/* files | Framework execution |

`to-issues` was merged into [[[pdlf:makepdlf-project-library/stepwise/step-19-to-tickets|Step 19 to Tickets]]](C:/pdlf/makepdlf-project-library/stepwise/step-19-to-tickets.md) at source and no longer exists under that name.
`to-prd` was renamed to `to-spec` at source and still exists, but PDLF's own pipeline does
not currently invoke it — no confirmed downstream consumer (the step that once used it,
old Step 13, was removed).

Ask which skill before starting any task (Hard Rule 8).

## Postgres ledger

PDLF progress is tracked in the `pdlf` database on localhost:5433 (Windows PostgreSQL 15, reached from WSL via `powershell.exe` bridge; WSL's own PostgreSQL 16 keeps port 5432). Role: `pdlf_agent`. Seven tables: projects, steps, gates, deviations, bft_records, isc, triage_findings. Never query or write this database directly unless executing a PDLF step that explicitly calls for it.

## Output governance

| Producer | Destination |
|---|---|
| GStack | `gstack-outputs/` |
| OpenCode | `opencode-outputs/` |
| Matt Pocock skills | `matt-skills-output/` |

File type overrides: docs → `docs-local/`, ADRs → `adr-local/`, wireframes → `wireframes/`, screens → `screens/`.

## Hard constraints

- Never write to `anvil.yaml`.
- No hardcoded colors — use CSS custom properties.
- Plan never writes. Build writes only with approval.
- `skill/SKILL.md` (the pre-decomposition monolithic file) is out of scope for dev-makepdlf —
  see AGENTS.md. Do not reference it as a live constraint.
- Do not write to PDLF-managed project code repos (mb-3-cs, mb4ecom, mb5pdlf) unless explicitly instructed.
