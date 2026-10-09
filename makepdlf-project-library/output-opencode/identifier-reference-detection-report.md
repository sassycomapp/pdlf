---
title: "identifier-reference-detection-report"
doc-id: "mb-6929faf4"
updated: "2026-10-09"
---
# Identifier-Reference Detection Report

**Scope:** `C:\dev\dev-makepdlf\makepdlf-project-library\` only.
**Excluded:** `pdlf-temp/`, `output-staging/` folder names (correct), `mb5pdlf` references, framework-usage of "PDLF".

---

## File: `.gbrain-source`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 1 | `dev-pdlf` (whole file) | `dev-makepdlf` | `dev-pdlf` |

---

## File: `AGENTS.md`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 1 | `# AGENTS.md — pdlf` | `# AGENTS.md — makepdlf` | Title line — `pdlf` as project name |

*(Line 70 `pdlf/` and line 81 `pdlf/` refer to the PDLF process artifacts folder — **framework, no change**.)*

---

## File: `INDEX.md`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 3 | `` C:\dev\dev-pdlf\ `` | `` C:\dev\dev-makepdlf\ `` | `Quick directory reference for ... Full map: docmap.md.` |

*(Line 119 `` pdlf/ `` is PDLF process artifacts folder — **framework, no change**.)*

---

## File: `README.md`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 41 | `` dev-pdlf-todo.md `` | `` dev-makepdlf-todo.md `` | `including the live ...` |

*(Lines 43, 44, 65, 67, 68 use `pdlf/` and `C:\pdlf\` and database `pdlf` — **all framework, no change**.)*

---

## File: `AGENTS-global-standard-backup.md`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 1 | `# AGENTS.md — dev-pdlf` | `# AGENTS.md — dev-makepdlf` | |
| 20 | `When dev-pdlf is concluded` | `When dev-makepdlf is concluded` | `...it will be migrated to and replace C:\pdlf\` |
| 276 | `read the entire dev-pdlf repo` | `read the entire dev-makepdlf repo` | `...and any PDLF-managed project repos` |
| 281 | `writes in dev-pdlf` | `writes in dev-makepdlf` | `...and only where the user has approved` |
| 356 | `with dev-pdlf's existing` | `with dev-makepdlf's existing` | `...documentation-standards rule.` |

*(Lines 31, 137, 229, 358 use `C:\pdlf\`, `docs/pre-pdlf/` — **framework, no change**.)*

---

## File: `instructions.md`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 3 | `` C:\dev\dev-pdlf\ `` (in text) | `` C:\dev\dev-makepdlf\ `` | `Agent instructions for working within the PDLF development workspace (...)` |
| 60 | `out of scope for dev-pdlf` | `out of scope for dev-makepdlf` | `...the pre-decomposition monolithic file) is` |

*(Lines 21, 32, 43 use `pdlf` in framework context — **no change**.)*

---

## File: `agents/instructions.md` (identical copy of `instructions.md`)

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 3 | `` C:\dev\dev-pdlf\ `` | `` C:\dev\dev-makepdlf\ `` | Same as above |
| 60 | `out of scope for dev-pdlf` | `out of scope for dev-makepdlf` | Same as above |

---

## File: `agents/domain.md`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 5 | `## PDLF's own domain (dev-pdlf workspace)` | `## PDLF's own domain (dev-makepdlf workspace)` | |

---

## File: `[[config]]`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 28 | `` /mnt/c/dev/dev-pdlf/ `` | `` /mnt/c/dev/dev-makepdlf/ `` | `Dev workspace ... PDLF development project` |
| 29 | `` /mnt/c/dev/dev-pdlf/stepwise/ `` | `` /mnt/c/dev/dev-makepdlf/stepwise/ `` | `Stepwise skills (source)` |
| 30 | `` /mnt/c/dev/dev-pdlf/templates-local/ `` | `` /mnt/c/dev/dev-makepdlf/templates-local/ `` | `Templates` |
| 38 | `` /mnt/c/dev/dev-pdlf/opencode.json `` | `` /mnt/c/dev/dev-makepdlf/opencode.json `` | `Config file ... Project-level` |
| 47 | `sassycomapp-dev-pdlf` | `sassycomapp-makepdlf` | `Project slug` |
| 48 | `~/.gstack/projects/sassycomapp-dev-pdlf/` | `~/.gstack/projects/sassycomapp-makepdlf/` | `GStack home` |
| 54 | `dev-pdlf` (as Source ID) | `dev-makepdlf` | `Source ID (dev-pdlf itself)` |
| 55 | `` /mnt/c/dev/dev-pdlf `` | `` /mnt/c/dev/dev-makepdlf `` | `Repo path` |

*(Lines 13, 18, 25, 26, 27, 81 use database `pdlf`, `C:\pdlf\`, `pdlf_agent` — **framework, no change**.)*

---

## File: `docs-local/docmap.md`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 13 | `` C:\dev\dev-pdlf\ `` | `` C:\dev\dev-makepdlf\ `` | `## Dev Workspace — ...` |
| 18 | `` C:\dev\dev-pdlf\ `` (tree root) | `` C:\dev\dev-makepdlf\ `` | Directory tree root |
| 131 | `dev-pdlf itself` | `dev-makepdlf itself` | `Matt Pocock skills config for ...` |
| 203 | `dev-pdlf's stepwise files` | `dev-makepdlf's stepwise files` | `Deployed copy of ...` |
| 210 | `` C:\dev\dev-pdlf\ `` | `` C:\dev\dev-makepdlf\ `` | `in the workshop only (...)` |

*(Lines 125, 136, 144, 195, 202, 218, 235, 242, 276, 331 use `C:\pdlf\`, `pdlf/`, `[[chk-pdlf-self-test]]`, database `pdlf` — **framework, no change**.)*

---

## File: `[[system-description]]`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 261 | `` C:\dev\dev-pdlf\ `` | `` C:\dev\dev-makepdlf\ `` | Directory tree root |
| 269 | `dev-pdlf itself` | `dev-makepdlf itself` | `Matt Pocock skills config for ...` |
| 310 | `` C:\dev\dev-pdlf\ `` | `` C:\dev\dev-makepdlf\ `` | `(...). Nothing has been deployed to C:\pdlf\` |

---

## File: `[[matt-pocock-skills-pdlf-compliance]]`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 43 | `` C:\dev\dev-pdlf\.scratch `` | `` C:\dev\dev-makepdlf\.scratch `` | `— exists` |
| 47 | `dev-pdlf` (occurrence 1) | `dev-makepdlf` | `...needs to run in exactly two places per project: ...` |
| 47 | `dev-pdlf` (occurrence 2) | `dev-makepdlf` | `...for building PDLF itself)` |

*(Line 44 references `mb5pdlf` — excluded, no change.)*

---

## File: `[[matt-pocock-skills-local-reference]]`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 3 | `within the dev-pdlf workspace` | `within the dev-makepdlf workspace` | `...Matt Pocock skills ...` |
| 61 | `dev-pdlf` (slug label) | `dev-makepdlf` | `\| dev-pdlf \| sassycomapp-dev-pdlf \|` |

**AMBIGUOUS — line 61 has two references:**
| 61 | `sassycomapp-dev-pdlf` | `sassycomapp-makepdlf` | Table cell: slug value |

*(Lines 53, 54, 60 reference `mb5pdlf` — excluded, no change.)*

---

## File: `[[deployment-procedure]]`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 12 | `` C:\dev\dev-pdlf\ `` | `` C:\dev\dev-makepdlf\ `` | `C:\dev\dev-pdlf\        C:\pdlf\stepwise\     ~/.config/opencode/` |
| 22 | `` C:\dev\dev-pdlf\stepwise\ `` | `` C:\dev\dev-makepdlf\stepwise\ `` | `Source: ... the canonical step skills` |
| 51 | `` /mnt/c/dev/dev-pdlf/stepwise/ `` | `` /mnt/c/dev/dev-makepdlf/stepwise/ `` | `cp -r ... /mnt/c/pdlf/stepwise/` |
| 57 | `` C:\dev\dev-pdlf\stepwise\ `` | `` C:\dev\dev-makepdlf\stepwise\ `` | `Copy-Item -Recurse ...` |
| 62 | `` /mnt/c/dev/dev-pdlf/stepwise/ `` | `` /mnt/c/dev/dev-makepdlf/stepwise/ `` | `cp ... step-11-init.md` |
| 71 | `` /mnt/c/dev/dev-pdlf/stepwise/ `` | `` /mnt/c/dev/dev-makepdlf/stepwise/ `` | `diff -r ...` |
| 103 | `` C:\dev\dev-pdlf\ `` | `` C:\dev\dev-makepdlf\ `` | `live in ...` |
| 107 | `## Relationship to dev-pdlf` | `## Relationship to dev-makepdlf` | Section heading |
| 109 | `` dev-pdlf\ `` (as folder name) | `` dev-makepdlf\ `` | `...is where PDLF is developed` |
| 111 | `dev-pdlf` (edit source) | `dev-makepdlf` | `...always edit the source in ...` |

---

## File: `specifications-local/spec-nomenclature.md`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 62 | `` C:\dev\dev-pdlf\ `` | `` C:\dev\dev-makepdlf\ `` | `PDLF dev workspace` |
| 97 | `` dev-pdlf `` (exception note) | `` dev-makepdlf `` | `...is a non-Anvil exception...` |
| 111 | `` dev-pdlf\stepwise\ `` | `` dev-makepdlf\stepwise\ `` | `## Stepwise File Naming (...)` |

*(Line 46 is a template example using `dev-{slug}\{slug}-project-library\` with a `mb5pdlf` example — **framework/no change**. Lines 61, 65, 105, 143 use `C:\pdlf\`, `pdlf/` — **framework, no change**.)*

---

## File: `[[adr-global-content-discovery-and-application-discipline]]`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 83 | `dev-pdlf ADR` | `dev-makepdlf ADR` | `...If GBrain semantic search proves...` |

---

## File: `[[renumbering-11-to-46]]`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 29 | `` C:\dev\dev-pdlf\skill\SKILL-v4.md `` | `` C:\dev\dev-makepdlf\skill\SKILL-v4.md `` | `...are now in sync.` |

---

## File: `[[chk-pdlf-self-test]]`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 5 | `dev-pdlf` | `dev-makepdlf` | `Tests C:\pdlf (and, until deployment, ...)` |

---

## File: `output-staging/instructions.md`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 1 | `dev-pdlf` (occurrence: project) | `dev-makepdlf` | `This is where dev-pdlf becomes pdlf` |

**AMBIGUOUS — same line, second occurrence:**
| 1 | `becomes pdlf` | **?** | `This is where dev-makepdlf becomes pdlf` — should `pdlf` here become `makepdlf` (the new repo/framework name), or stay `pdlf` (the deployed framework)? **Needs user decision.** |

---

## File: `[[step-11-build-notes]]`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 14 | `Stays in dev-pdlf` | `Stays in dev-makepdlf` | `as project build history` |
| 45 | `dev-pdlf versus` | `dev-makepdlf versus` | `docs-local inside ...` |
| 133 | `` dev-pdlf and C:\pdlf `` | `` dev-makepdlf and C:\pdlf `` | `are both excluded` |

---

## File: `[[step-11-init]]`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 88 | `` dev-pdlf or C:\pdlf `` | `` dev-makepdlf or C:\pdlf `` | `This item does not apply to ...` |

---

## File: `[[step-11-project-inventory-build-notes]]`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 27 | `` dev-pdlf `` (project entry) | `` dev-makepdlf `` | `has a manually-added entry` |

---

## File: `stepwise/step-11-decision-tree-v2.html`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 56 | `dev-pdlf or C:\pdlf` | `dev-makepdlf or C:\pdlf` | `Not applied to ...` |

---

## File: `[[step-16-build-notes]]`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 55 | `` dev-pdlf `` (itself) | `` dev-makepdlf `` | `not just for ...` |

---

## File: `wip/dev-pdlf-todo.md`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 21 | `dev-pdlf's own housekeeping` | `dev-makepdlf's own housekeeping` | `out of scope for ...` |

*(Note: the filename `dev-pdlf-todo.md` also needs renaming to `dev-makepdlf-todo.md` (dev-makepdlf wip).)*

---

## File: `wip/Active PDF To Do List has been save.txt`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 1 | `` C:\dev\dev-pdlf\wip\ToDo.md `` | `` C:\dev\dev-makepdlf\wip\ToDo.md `` | `Active PDF To Do List has been saved as:` |
| 3 | `` C:\dev\dev-pdlf\wip\ `` | `` C:\dev\dev-makepdlf\wip\ `` | `Active non PDLF To Do List has been saved as...` |
| 13 | `dev-pdlfscaffold` | `dev-makepdlfscaffold` | `take a long look at the ... nd associated documents` |
| 15 | `dev-pdlf project folders` | `dev-makepdlf project folders` | `examine all the remaining docs in the ...` |

---

## File: `wip/Active-non-PDLF-ToDo-List.md`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 35 | `` dev-pdlf `` (reference to project) | `` dev-makepdlf `` | `...not dev-pdlf's. If you'd rather` |

*(Line 33 references `todo-pdlf.md` — this is a filename reference. See ambiguous cases below.)*

---

## File: `obsolete/dev-pdlf-scaffold.md`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 1 | `# dev-pdlf Scaffold Snapshot` | `# dev-makepdlf Scaffold Snapshot` | Title |

*(Lines 40-87 contain `pre-pdlf/`, `todo-pdlf.md` — framework/historical filenames. See ambiguous section.)*

*(Note: the filename `dev-pdlf-scaffold.md` also contains the old identifier but is in `obsolete/` — renaming may be optional.)*

---

## File: `obsolete/session-handover.md`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 13 | `` dev-pdlf `` (both in bold and path) | `` dev-makepdlf `` | `1. **dev-pdlf** (C:\dev\dev-pdlf\) — the workshop.` |
| 13 | `` C:\dev\dev-pdlf\ `` | `` C:\dev\dev-makepdlf\ `` | `same line, path` |

---

## File: `obsolete/session-decisions-and-learnings.md`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 16 | `dev-pdlf` | `dev-makepdlf` | `...and C:\pdlf are permanent exceptions.` |
| 46 | `dev-pdlf` | `dev-makepdlf` | `...is a non-Anvil exception...` |

---

## File: `workspace/gbrain/README.md`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 1 | `# GBrain Integration — dev-pdlf` | `# GBrain Integration — dev-makepdlf` | Title |
| 10 | `` dev-pdlf `` (source name) | `` dev-makepdlf `` | `registered as the ... source` |
| 14 | `--source dev-pdlf` | `--source dev-makepdlf` | `gbrain sync ...` |
| 14 | `` /mnt/c/projects/dev-pdlf `` | `` /mnt/c/projects/makepdlf `` | `--repo ... --yes` |

---

## File: `workspace/gstack/README.md`

| Line | Match | Replacement | Context |
|------|-------|-------------|---------|
| 1 | `# GStack Integration — dev-pdlf` | `# GStack Integration — dev-makepdlf` | Title |
| 6 | `dev-pdlf project` | `dev-makepdlf project` | `configured for the ...` |

---

## Files with NO matches to fix:

- `opencode.json` — clean
- `.gitignore` — clean
- `.env` — clean
- `policy-local/*` — only `pdlf/` folder references (framework), no project references
- `[[spec-bft]]`, `[[spec-execution-discipline]]`, `[[spec-gate-procedure]]`, `[[spec-postgres-ledger]]`, `[[spec-skill-design]]` — only framework `pdlf` references (database, `pdlf/` folder paths in templates), no project references
- `templates-local/*` — only `pdlf/` folder paths in templates (framework)
- `stepwise/step-12*` through `stepwise/step-46*` (excluding steps 11, 16) — only `pdlf/` folder in templates (framework), no project references
- `wip/workflow.md` — only `pdlf/` folder paths in templates (framework)
- `pre-project/` — `pdlf` refers to the PDLF framework/process, not this project

---

## Ambiguous / Questionable Items

| File | Line | Text | Question |
|------|------|------|----------|
| `output-staging/instructions.md` | 1 | `dev-pdlf becomes pdlf` | The 2nd `pdlf` — should it become `makepdlf` (new repo name) or stay `pdlf` (naming the deployed framework)? |
| `wip/Active-non-PDLF-ToDo-List.md` | 33 | `todo-pdlf.md` | This is a reference to a project-specific filename. Rename reference to `todo-makepdlf.md`? |
| `obsolete/dev-pdlf-scaffold.md` | (filename + contents) | `dev-pdlf-scaffold.md`, `pre-pdlf/`, `todo-pdlf.md` | All in `obsolete/` — rename filename and update internal references, or leave as historical? |
| `wip/dev-pdlf-todo.md` | (filename) | `dev-pdlf-todo.md` | Rename file to `dev-makepdlf-todo.md` (dev-makepdlf wip)? Also update its content line 21. |
| `README.md` | 41 | `dev-pdlf-todo.md` | Update reference to `dev-makepdlf-todo.md` (dev-makepdlf wip)? |
| `AGENTS.md` | 1 | `# AGENTS.md — pdlf` | Replace standalone `pdlf` (project name in title) with `makepdlf`? |

---

## Summary Counts

| Category | Count |
|----------|-------|
| `dev-pdlf` → `dev-makepdlf` replacements | ~52 occurrences across 20+ files |
| `C:\dev\dev-pdlf\` → `C:\dev\dev-makepdlf\` path replacements | ~16 occurrences (overlaps with above) |
| `/mnt/c/dev/dev-pdlf/` → `/mnt/c/dev/dev-makepdlf/` path replacements | ~8 occurrences |
| `sassycomapp-dev-pdlf` → `sassycomapp-makepdlf` | 2 occurrences |
| `/mnt/c/projects/dev-pdlf` → `/mnt/c/projects/makepdlf` | 1 occurrence |
| Filename renames needed (`dev-pdlf-todo.md` → `dev-makepdlf-todo.md` (dev-makepdlf wip)) | 1 file + 1 reference |
| Ambiguous (needs decision) | ~6 items |

---

**No `pdlf-project-library` references were found** that need fixing — all 5 matches were for `mb5pdlf-project-library` (unrelated project, correctly left alone).
