---
title: "step-11-project-inventory-build-notes"
doc-id: "mb-1040ef12"
updated: "2026-10-10"
---
# Step 11 — project-inventory.md Integration — Build Notes

**Status: fulfilled.** Kept
here as the record of why, not as a pending task.

**Destination:** `[[step-11-init]]`. Added alongside the existing registry-write action
(`C:\pdlf\registry\projects.json`) — this is functionally a second registry, focused on
path/credential verification rather than PDLF run state.

## The rule

`project-inventory.md` lives at `C:\dev\dev-root\project-inventory.md` — authoritative reference
for path/credential correctness across all projects.

Every Step 11 run, for either entry mode, does this against it:

1. Check whether the current project already has an entry.
2. **No entry** — add one, once Step 11 has established the real local paths, GitHub
   URLs, GBrain source names, and GStack path for this project. Applies to a genuinely
   new project and to a legacy project getting its first-ever entry.
3. **Entry exists** — verify it against what's actually there right now (local paths,
   GitHub URLs, GBrain sources, GStack path). Any mismatch is surfaced to the developer
   directly — never silently accepted, never silently overwritten.

## Exceptions — confirmed

- `dev-makepdlf` — has a manually-added entry, made before PDLF existed to run Step 11
  against anything. Left alone. Not something Step 11 ever touches.
- `C:\pdlf` — never gets an entry. It's the deployed tool, not a project PDLF builds.

## Dependency — corrected

The GBrain source-scoping rule now lives in [[[pdlf:pdlf-library/policy-local/pol-memory-and-knowledge|Policy: Memory and Knowledge]]](C:/pdlf/pdlf-library/policy-local/pol-memory-and-knowledge.md) (the earlier
reference to a "the retired `spec-execution-discipline-build-notes.md`" was to a file that was
mis-categorized and later retired — the rule was properly relocated into that policy,
not left as a standalone note). That policy can now use this file's `project-inventory.md`
integration as the authoritative lookup for exact GBrain source names.
