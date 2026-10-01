---
title: "pdlf-spec-nomenclature"
doc-id: "mb-4c33cf0d"
updated: "2026-10-01"
---
# PDLF — Nomenclature Specification

Canonical naming rules for the PDLF system: project slugs, the GStack-derived
project names, copy filenames, folder names per environment, and document
identity. Implements decisions 5, 8, 9, and 10 of
`pdlf-adr-artifact-saving-convention`. Facts marked "verified 2026-09-11"
were checked against the live environment on that date.

---

## 1. The project slug — the canonical short name

Every PDLF project has one canonical short slug, supplied by the developer at
Step 11 (item 2 of that step) and used everywhere else:

- Folder names: `C:\dev\dev-{slug}\`, `{slug}` (code repo),
  `{slug}-project-library` (docs repo).
- Ledger: the `projects` row's `slug` field.
- Every PDLF path template in the step files: `dev-{slug}\{slug}-project-library\…`.
- Safety-net copy filenames: `{slug}-filename` (§4).

For the PDLF system's own builder project, the slug is `makepdlf`.

This slug is the single name the developer and every project document use.
Nothing else in the naming system may contradict it.

## 2. The GStack-derived project names — deterministic, not chosen

GStack skills do not use the project slug directly. Each skill run resolves a
project name from the git repository it runs in. Verified 2026-09-11 from the
current `gstack-slug` source:

1. **Cache first:** a saved value keyed by the exact absolute working
   directory (`~/.gstack/slug-cache/<encoded-cwd>`).
2. **Otherwise, the git remote:** `git remote get-url origin`, parsed to
   `org-repo` form, slashes turned to dashes.
3. **Otherwise, the directory name** (basename of the working directory).

The output is sanitized to `[a-zA-Z0-9._-]` and cached atomically for future
runs. The branch name (`BRANCH`) is resolved alongside (`SLUG`, `BRANCH`).

### 2.1 The invariant

Step 11 creates each project's GitHub docs repo under the fixed name
`{slug}-project-library` in the sassycomapp organization. Therefore, for any
skill run in a project's docs repo:

    gstack slug = sassycomapp-{slug}-project-library

And for any skill run in the project's code repo (remote
`sassycomapp/{slug}`):

    gstack slug = sassycomapp-{slug}

**A project therefore has two GStack names — one per repository.** Which one
applies depends on which repo a skill runs in, not on preference. Built steps
11–16 run in the docs repo, so their native saves derive
`sassycomapp-{slug}-project-library`; build-loop skills (QA, review) run in
the code repo and derive `sassycomapp-{slug}`. Any document or module that
states a native path must state which repository it means.

This invariant is what makes "no ambiguity about project names" true by
construction: the name is derived from a repo name PDLF itself fixed, not
resolved per-run by context.

## 3. Cache hygiene — the known weakness and its rule

The cache is keyed by the exact working directory and is never reconciled
against the git remote (verified 2026-09-11). A renamed or re-cloned
repository can therefore keep serving its old name forever — observed live on
a placeholder project, whose cache held a name neither the remote nor the
existing artifact folders used.

Rules:

- The cache is never hand-edited casually.
- A verified divergence (cache value ≠ remote-derived value for the same
  directory) is healed by writing the remote-derived value into the cache
  entry, with the developer's explicit permission, and recorded.
- Because the orchestrator pastes artifacts rather than relying on skill
  searches (handoff contract), a stale cache degrades the safety net, not the
  chain — but it is still healed when found.

## 4. Copy filenames — `{slug}-filename`

Every safety-net and stable copy carries the canonical short slug as a
filename prefix: `{slug}-step-NN-filename.md` (example:
`makepdlf-step-14-ceo-plan.md`). The slug used is the §1 canonical short
slug — not the longer GStack-derived name, which is a derived fact, not a
filename basis.

## 5. Folder names per environment

| Layer / phase | Folder | Notes |
|---|---|---|
| PDLF environment — safety net | `C:\pdlf\output\pdlf-output-gstack\`, `pdlf-output-pocock\`, `pdlf-output-opencode\` (when created) | Producer-routed; serves the one active project |
| makePDLF environment — exception phase | `output-gstack\`, `output-opencode\`, `output-matt-skills\` inside the makepdlf docs repo | Per that project's own artifact governance; `output-staging\` exists but is unrouted |
| Built step files 14–15 (legacy) | `gstack-outputs\` | Corrected to `output-gstack\` under convention adoption (tracked: master task list, item 18) |

Folder names are deliberately per-environment: the binding rule is the
routing pattern (producer-routed copies, `{slug}-filename`, copy-first-then-
clear), not one universal folder name.

## 6. Document identity and numbering exceptions

- Every document in `pdlf-library` carries the `pdlf-` prefix plus its type
  (`pdlf-adr-`, `pdlf-spec-`, `pdlf-pol-`, `pdlf-proc-`, `pdlf-expl-`), so
  its doc-id (the filename) is unique across the whole corpus by construction
  and its home is discoverable from the name alone.
- Files are named descriptively without sequence numbers (per the global
  filename-and-numbering policy). Two standing exceptions are inherently
  ordinal and keep their numbers: the stepwise material (steps 1–46, with
  retired numbers left as reserved gaps — e.g. step 13) and the app-factory
  modules (module-1 … module-46), which mirror the steps one-to-one.

---

*End of pdlf-spec-nomenclature*