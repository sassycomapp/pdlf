---
title: "matt-pocock-skills-local-reference"
doc-id: "mb-b97bfee0"
updated: "2026-10-24"
---
# PDLF — Matt Pocock Skills Local Reference

**What this is:** how PDLF uses Matt Pocock's skills: their role, where they are set up, where their outputs go, and the rules for using them. The skills are pinned at `5beb35b` of `mattpocock/skills` (MIT licence), cloned at `C:\mybizz\matt-pocock-skills-source`.

---

## Layer roles

| Layer | Tool | Role |
|---|---|---|
| Orchestration | PDLF | The full project lifecycle, stage-gated |
| Workflow | GStack | Planning reviews, QA, review, ship |
| Engineering discipline | Matt Pocock skills | Domain modeling, tickets, triage, architecture |
| Memory | GBrain | Persistent knowledge base |

---

## Where the skills are used

Each step that uses a Matt Pocock skill records it in its own build plan and config: Steps 16, 19, 39 and 40.

`setup-matt-pocock-skills` runs once per project library, at Step 11, with PDLF's answers fixed in advance ([[[pdlf:app-factory/phase-b-discover-and-define/b11-build-plan|Step 11 Build Plan]]](C:/pdlf/app-factory/phase-b-discover-and-define/b11-build-plan.md)): tickets are local markdown files in `pdlf-tickets\`; the five standard triage labels; a single context, with the glossary at `docs-local\GLOSSARY.md` and decisions in `adr-local\`. It writes the `## Agent skills` block into the project library's `AGENTS.md` and its configuration files into `docs\agents\`, and never creates a `CLAUDE.md`. The code repositories need no setup: no Matt Pocock skill writes into them.

---

## Where the outputs go

| Skill | Destination |
|---|---|
| [[[pdlf:app-factory/phase-b-discover-and-define/b16-reference\|Step 16 Domain Modeling]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-reference.md), `grill-with-docs` | `docs-local\GLOSSARY.md` and `adr-local\` |
| [[[pdlf:app-factory/phase-c-design-and-plan/c19-reference\|Step 19 to Tickets]]](C:/pdlf/app-factory/phase-c-design-and-plan/c19-reference.md) | `pdlf-tickets\`, one file per ticket |
| `triage` | The ledger's `triage_findings` table |
| `setup-matt-pocock-skills` | `docs\agents\` and the `## Agent skills` block of `AGENTS.md` |
| [[[pdlf:app-factory/phase-e-build-and-verify/e40-reference\|Step 40 Improve Codebase Architecture]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40-reference.md) | As its build plan sets out |

---

## Rules

1. **Read the skill's own file before invoking it.** A skill's name is never trusted on its own; reading it shows whether it is a thin wrapper and what it depends on.
2. **A thin wrapper needs every skill it names.** If a skill's body only delegates to other skills, each of them must be installed, or the invocation does nothing.
3. **User-invoked skills are asked for.** The agent asks David to start such a skill; it never starts or simulates it itself.
4. **Pinned, not live.** The skills are copied files at a pinned version; upstream changes never arrive by themselves. A version change is David's decision, and the steps that use the skills are checked against it first.

---

## Why these skills

Matt Pocock's skills are small and composable, so PDLF takes only the few it needs. Whole-lifecycle frameworks (BMAD-METHOD, GitHub Spec Kit, OpenSpec, GSD, Superpowers) were assessed and rejected: each is a complete orchestration system that would compete with PDLF itself (its ledger, gates and orchestrator), not a library a step can draw one skill from.
