---
title: "matt-pocock-skills-pdlf-compliance"
doc-id: "mb-86e5409b"
updated: "2026-10-12"
---
# Matt Pocock Skills — PDLF Compliance & Dependency Reference
**Supersedes the earlier general-catalog audit. Scoped to the 5 skills PDLF actually uses.**
**Source: mattpocock/skills v1.1.0 (MIT licensed). No Claude Code references — PDLF runs on OpenCode.**

---

## 0. Skills actually in scope

| Skill | Used at | Type | Wrapper or Fat |
|---|---|---|---|
| `setup-matt-pocock-skills` | Once per repo, before any other engineering skill | User-invoked | Fat (config generator) |

Skills used at a particular step are recorded in that step's config (Steps 16, 19, 39 and 40).

`to-spec`/`to-prd` and `prototype` are correctly removed — no action needed, and their absence doesn't break anything since nothing downstream consumes them. `to-issues` is a stale name for [[[pdlf:app-factory/phase-c-design-and-plan/c19-reference|Step 19 to Tickets]]](C:/pdlf/app-factory/phase-c-design-and-plan/c19-reference.md); fix the artifact governance table.

---

## 1. Compliance checklist — full list

1. Run `/setup-matt-pocock-skills` once per repo, before the first use of any other engineering skill in that repo. It is prompt-driven (explores, presents findings, confirms with you, then writes) — never a blind scaffold.
2. It writes an `## Agent skills` block into that repo's AGENTS.md (PDLF already standardizes on `AGENTS.md`, not `CLAUDE.md` — correct, keep it that way).
3. It writes three config files under `docs/agents/` in Matt Pocock's own default layout.
   **PDLF's actual location, confirmed this session: `agents/` at the repo root** — not
   `docs/agents/`, and not `docs-local/agents/` as an earlier draft of this document
   guessed. The raw, unedited `docs/agents/` template output was found duplicated
   alongside the real, customized `agents/` folder and retired to `obsolete/`.
4. **Read the skill's own file before invoking it — never trust the name alone.** This is already PDLF principle #6; it happens to be the exact discipline that identifies wrapper-vs-fat and hidden dependencies.
5. If a skill is a thin wrapper (body is a one-line delegation to other skill names), every skill it names must also be present, or the invocation does nothing useful.
6. Re-running setup is only needed to switch issue tracker or start over. Day-to-day changes are direct edits to the `docs/agents/*.md` files it produced.
7. **When the model needs to use a user-invoked skill, it must ask the developer to invoke it — never invoke it itself, never simulate it.** This preserves PDLF's "agent makes no decisions" principle and keeps the pipeline from silently branching.
8. MIT license — no attribution requirement, but worth a one-line credit in PDLF's own docs given how much of the engineering-discipline layer depends on it.
9. Skills are copied files (not a live plugin), so upstream updates from Matt Pocock do not propagate automatically. Recommend a periodic manual diff against upstream `main` for the 5 skills in use, rather than assuming they stay current.

---

## 2. Open items requiring your input

### A. Which repo(s) need `setup-matt-pocock-skills` — RESOLVED
Confirmed `.scratch/` locations:
- `C:\dev\dev-mb5pdlf\mb5pdlf-project-library\.scratch` — exists
- `C:\dev\dev-mb5pdlf\mb5pdlf` (code repo) — **no `.scratch`**

All four in-pipeline skills ([[[pdlf:app-factory/phase-b-discover-and-define/b16-reference|Step 16 Domain Modeling]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-reference.md), [[[pdlf:app-factory/phase-c-design-and-plan/c19-reference|Step 19 to Tickets]]](C:/pdlf/app-factory/phase-c-design-and-plan/c19-reference.md), `triage`, [[[pdlf:app-factory/phase-e-build-and-verify/e40-reference|Step 40 Improve Codebase Architecture]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40-reference.md)) currently write into the **project-library (docs) repo**, not the code repo. So `setup-matt-pocock-skills` needs to run in exactly two places per project: `pdlf` (for building PDLF itself) and `{project}-project-library` (for all four in-pipeline skills). **The code repo does not need setup run in it** — nothing currently writes Matt Pocock output there. Re-check this if a future skill is added that writes directly into the code repo.

### B. The `grilling` dependency gap — RESOLVED, no import
Held in the build plans of Steps 39 and 40, the steps it concerns.

### C. Stale table entry — orphaned reference
This originally pointed to "a separate correction instruction file for the exact edit."
That file is not present in the current document set. Either it was never delivered, or
it's been lost. Flagged rather than silently dropped — content of the original correction
is unknown.

### D. `triage` state-machine duplication — RESOLVED
Held in Step 39's build plan, the step it concerns.

---

## 3. Framework-alternative research (completed)

Evaluated: BMAD-METHOD, GitHub Spec Kit, OpenSpec, GSD, Superpowers.

**Verdict: keep the extracted Matt Pocock skills. Don't switch.**

- These frameworks are complete orchestration systems (BMAD alone coordinates 12+ specialized agents across the full SDLC), not atomic skill libraries. They compete with **PDLF itself** — the ledger, the gates, the stepwise orchestrator — not with the four narrow skills sitting inside it. Adopting one would mean discarding PDLF's own orchestration layer, a far bigger move than anything currently in question.
- They're also not designed to be raided for individual parts the way Matt Pocock's repo is — his skills are explicitly small and composable; theirs are choreographed as a whole. That's why you were able to cleanly extract 4 skills and drop the rest — the same move isn't available against BMAD/GSD/Spec Kit.
- The one framework worth a mental bookmark, not a switch: **Superpowers**, a TDD-enforced discipline system — relevant only if PDLF's own Step 35 three-level testing methodology is ever reconsidered. Not relevant today.
- `triage`'s label state machine remains the one legitimate internal condensation candidate — folding it into the Postgres ledger (`steps`/`gates` tables) rather than maintaining a second, file-based state system — worth a design pass on its own, separate from this framework question.

---

*Reference v2 — supersedes the general-catalog version. Reconciled against [[[pdlf:obsolete/system-description|System Description]]](C:/pdlf/obsolete/system-description.md) (v3.1) and [[[pdlf:pdlf-library/docs-local/matt-pocock-skills-local-reference|Matt Pocock Skills Local Reference]]](C:/pdlf/pdlf-library/docs-local/matt-pocock-skills-local-reference.md).*
