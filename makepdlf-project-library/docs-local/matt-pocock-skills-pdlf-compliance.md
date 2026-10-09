---
title: "matt-pocock-skills-pdlf-compliance"
doc-id: "mb-86e5409b"
updated: "2026-10-09"
---
# Matt Pocock Skills — PDLF Compliance & Dependency Reference
**Supersedes the earlier general-catalog audit. Scoped to the 5 skills PDLF actually uses.**
**Source: mattpocock/skills v1.1.0 (MIT licensed). No Claude Code references — PDLF runs on OpenCode.**

---

## 0. Skills actually in scope

| Skill | Used at | Type | Wrapper or Fat |
|---|---|---|---|
| `setup-matt-pocock-skills` | Once per repo, before any other engineering skill | User-invoked | Fat (config generator) |
| [[[pdlf:makepdlf-project-library/stepwise/step-16-domain-modeling\|Step 16 Domain Modeling]]](C:/pdlf/makepdlf-project-library/stepwise/step-16-domain-modeling.md) | Step 16 (invoked via `/grill-with-docs`) | Model-invoked | Fat, self-contained |
| [[[pdlf:makepdlf-project-library/stepwise/step-19-to-tickets\|Step 19 to Tickets]]](C:/pdlf/makepdlf-project-library/stepwise/step-19-to-tickets.md) | Step 19 | User-invoked | Fat, self-contained |
| `triage` | Step 39 | User-invoked | Fat, **has an unresolved dependency — see §2** |
| [[[pdlf:makepdlf-project-library/stepwise/step-40-improve-codebase-architecture\|Step 40 Improve Codebase Architecture]]](C:/pdlf/makepdlf-project-library/stepwise/step-40-improve-codebase-architecture.md) | Step 40 (optional) | User-invoked | Fat, **has an unresolved dependency — see §2** |

`to-spec`/`to-prd` and `prototype` are correctly removed — no action needed, and their absence doesn't break anything since nothing downstream consumes them. `to-issues` is a stale name for [[[pdlf:makepdlf-project-library/stepwise/step-19-to-tickets|Step 19 to Tickets]]](C:/pdlf/makepdlf-project-library/stepwise/step-19-to-tickets.md); fix the artifact governance table.

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
- `C:\dev\dev-makepdlf\.scratch` — exists
- `C:\dev\dev-mb5pdlf\mb5pdlf-project-library\.scratch` — exists
- `C:\dev\dev-mb5pdlf\mb5pdlf` (code repo) — **no `.scratch`**

All four in-pipeline skills ([[[pdlf:makepdlf-project-library/stepwise/step-16-domain-modeling|Step 16 Domain Modeling]]](C:/pdlf/makepdlf-project-library/stepwise/step-16-domain-modeling.md), [[[pdlf:makepdlf-project-library/stepwise/step-19-to-tickets|Step 19 to Tickets]]](C:/pdlf/makepdlf-project-library/stepwise/step-19-to-tickets.md), `triage`, [[[pdlf:makepdlf-project-library/stepwise/step-40-improve-codebase-architecture|Step 40 Improve Codebase Architecture]]](C:/pdlf/makepdlf-project-library/stepwise/step-40-improve-codebase-architecture.md)) currently write into the **project-library (docs) repo**, not the code repo. So `setup-matt-pocock-skills` needs to run in exactly two places per project: `dev-makepdlf` (for building PDLF itself) and `{project}-project-library` (for all four in-pipeline skills). **The code repo does not need setup run in it** — nothing currently writes Matt Pocock output there. Re-check this if a future skill is added that writes directly into the code repo.

### B. The `grilling` dependency gap — RESOLVED, no import
Two of your five in-scope skills have documented branches into the `grilling` interview loop:
- [[[pdlf:makepdlf-project-library/stepwise/step-40-improve-codebase-architecture|Step 40 Improve Codebase Architecture]]](C:/pdlf/makepdlf-project-library/stepwise/step-40-improve-codebase-architecture.md) — ends with "...then grill through whichever one you pick."
- `triage` — independently documented as "categorise, verify, **grill if needed**, and write agent-ready briefs."

Neither `grilling` nor its wrappers (`grill-me`, `grill-with-docs`) will be imported. Tested against the one selection criterion PDLF actually uses — does this fit a real need OpenCode can't already do itself — it fails: PDLF's own execution discipline already has an equivalent mechanism (a step that can't complete presents a deviation request with three options, never deciding unilaterally). **Action: route the "grill if needed" branches in `triage` and [[[pdlf:makepdlf-project-library/stepwise/step-40-improve-codebase-architecture|Step 40 Improve Codebase Architecture]]](C:/pdlf/makepdlf-project-library/stepwise/step-40-improve-codebase-architecture.md) into PDLF's existing deviation-request flow instead of a Matt Pocock skill.** `grill-with-docs` was considered and rejected specifically — it's user-invoked only (`disable-model-invocation: true`), so it can't fire automatically mid-step in the first place, and it redundantly bundles in [[[pdlf:makepdlf-project-library/stepwise/step-16-domain-modeling|Step 16 Domain Modeling]]](C:/pdlf/makepdlf-project-library/stepwise/step-16-domain-modeling.md), which PDLF already runs standalone at Step 16.

### C. Stale table entry — orphaned reference
This originally pointed to "a separate correction instruction file for the exact edit."
That file is not present in the current document set. Either it was never delivered, or
it's been lost. Flagged rather than silently dropped — content of the original correction
is unknown.

### D. `triage` state-machine duplication — RESOLVED, and now confirmed shipped

**Solution: treat `triage` as a pure computation step feeding the ledger, exactly like Step 38A already does for CI results.** This is not a new pattern — it's the same consolidation precedent your own pipeline already established one step earlier in the same loop.

**Status update:** this proposal is no longer just a recommendation — `triage_findings` is
a live table in [[[pdlf:makepdlf-project-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-postgres-ledger.md)'s current seven-table schema, with exactly the
columns proposed below. This section is kept for its rationale, not as an open action item.

1. Add a `triage_findings` table to the `pdlf` ledger: one row per finding, scoped to the feature's Step 39 row. Columns: `finding_id`, `source_step` (36/37/38), `triage_label` (Matt's existing five values — `needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`; no new vocabulary), `resolution_note`, `resolved_by`, `resolved_at`.
2. Step 39 runs `triage`, gets its label output in `.scratch/`, and immediately upserts it into `triage_findings`. Per the Step Receipt principle (the receipt IS the ledger row, not a gloss), the triage label IS the `triage_label` column — not a standing file.
3. The `.scratch/` output is transient computation input, consumed once — same status as raw CI logs at 38A, not treated as authoritative afterward.
4. `build-verified` gate evaluation becomes a pure ledger query: passes only when every `triage_findings` row for that feature is `wontfix` or has a non-null `resolved_at`. Consistent with principle 3 and with how every other gate in the system is FK-enforced rather than file-checked.

---

## 3. Framework-alternative research (completed)

Evaluated: BMAD-METHOD, GitHub Spec Kit, OpenSpec, GSD, Superpowers.

**Verdict: keep the extracted Matt Pocock skills. Don't switch.**

- These frameworks are complete orchestration systems (BMAD alone coordinates 12+ specialized agents across the full SDLC), not atomic skill libraries. They compete with **PDLF itself** — the ledger, the gates, the stepwise orchestrator — not with the four narrow skills sitting inside it. Adopting one would mean discarding PDLF's own orchestration layer, a far bigger move than anything currently in question.
- They're also not designed to be raided for individual parts the way Matt Pocock's repo is — his skills are explicitly small and composable; theirs are choreographed as a whole. That's why you were able to cleanly extract 4 skills and drop the rest — the same move isn't available against BMAD/GSD/Spec Kit.
- The one framework worth a mental bookmark, not a switch: **Superpowers**, a TDD-enforced discipline system — relevant only if PDLF's own Step 35 three-level testing methodology is ever reconsidered. Not relevant today.
- `triage`'s label state machine remains the one legitimate internal condensation candidate — folding it into the Postgres ledger (`steps`/`gates` tables) rather than maintaining a second, file-based state system — worth a design pass on its own, separate from this framework question.

---

*Reference v2 — supersedes the general-catalog version. Reconciled against [[[pdlf:makepdlf-project-library/docs-local/system-description|System Description]]](C:/pdlf/makepdlf-project-library/docs-local/system-description.md) (v3.1) and [[[pdlf:makepdlf-project-library/docs-local/matt-pocock-skills-local-reference|Matt Pocock Skills Local Reference]]](C:/pdlf/makepdlf-project-library/docs-local/matt-pocock-skills-local-reference.md).*
