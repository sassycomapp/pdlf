---
title: "step-11-init"
doc-id: "mb-f862ee91"
updated: "2026-10-12"
---
## Task Execution Order

1. Ask the developer: is this a new project or an existing project?
2. Ask the developer for the project slug.
3. Verify the Postgres ledger is reachable. Confirm the `pdlf` database and all six
   tables (`projects`, `steps`, `gates`, `deviations`, `bft_records`, `isc`) exist. Use
   the WSL→Windows bridge pattern (see Reference).
4. → If **new project**: follow items 5–10, then continue at item 16.
   → If **existing project**: skip to item 11.

### New-project entry

5. Ask the developer for the GitHub code repo URL.
6. → Decision point: if no URL is available, instruct the developer to set up the app in
   Anvil first — Anvil creates the code repo automatically when the app is created there
   — then provide the URL. Repeat item 5 until a URL is supplied. The agent never
   creates the code repo itself.
7. Copy the project template from `C:\dev\project-template\dev-(SLUG)\` to
   `C:\dev\dev-{slug}\`, applying slug substitution throughout — folder names and file
   contents, including AGENTS.md, README.md, CLAUDE.md, opencode.json.
8. Link the GitHub code repo to the local code repo at `dev-{slug}\{slug}\`.
9. → Decision point: ask the developer's permission to create a new GitHub repository,
   `{slug}-project-library`, for the docs repo. On approval, create it and link it to the
   local docs repo at `dev-{slug}\{slug}-project-library\`.
10. Ask the developer to supply the three pre-project files (`[[01-project-brief]]`,
    `[[02-scoping-ideas]]`, `[[03-constraints-and-notes]]`) with content specific to this
    project, and to place them into
    `dev-{slug}\{slug}-project-library\pre-project\`. Other project-specific material
    goes into the appropriate canonical folder, not `pre-project\`.

### Existing-project entry

11. Ask the developer for: the GitHub code repo URL, the GitHub docs repo URL, the local
    code repo path, and the local docs repo path.
12. Compare the local docs repo's folder structure against the canonical folder list
    (see the template at `C:\dev\project-template\dev-(SLUG)\project-library\`). Create
    only the folders that are genuinely missing. Never modify, move, or overwrite
    anything already present. Do not add an `Instructions.md` file to any folder created
    here — a standing freeze is in effect on creating further `Instructions.md` files
    anywhere, until a decided format lands.
13. → Decision point: inspect the GitHub code repo. Verify the GitHub↔local link for
    both the code repo and the docs repo. If either link is broken or missing, ask the
    developer's permission before correcting it.
14. → Decision point: verify the GBrain registration for both the code repo and the docs
    repo. If either is missing, ask the developer's permission before establishing it.
15. Ask the developer to confirm the data integrity of the local code repo and the local
    docs repo.

### Convergence — common to both entry modes

16. Update the local [[[makepdlf-project-library:agents|AGENTS.md]]](C:/dev/dev-makepdlf/makepdlf-project-library/AGENTS.md) in the docs repo. Set up system files: `.git`,
    `.gitignore`, `.opencode`, GStack configuration. Set up Matt Pocock skills
    configuration.
17. Register the GBrain doc source for `{slug}` and the GBrain code source for
    `{slug}-code`, if not already registered — this adds the source only; it does not
    sync or embed.
17a. Check whether `project-library-global` is already registered as a GBrain source. If
    not, register it. Runs every Step 11 invocation, regardless of entry mode —
    `project-library-global` is shared infrastructure, not per-project, so this is not a
    one-time bootstrap tucked elsewhere; Step 11 is where it's verified every time.
18. → Decision point: ask the developer's permission to commit and push both repos now,
    as an early check that the setup is correct. If approved, do so and surface any
    errors immediately. If declined, proceed — this is not repeated automatically later;
    it is asked again as ordinary housekeeping at item 22.
19. → Decision point: ask the developer's permission to use the `mb-submit-memory`
    skill now, against any real, developer-written content produced so far, as the same
    kind of early check. If approved, invoke `/mb-submit-memory (path)` for each real
    file, using the `pdlf_step_sync` credential — this is a PDLF step's own routine
    housekeeping, not a developer's independent, ad-hoc request, and the credential
    used must say so honestly — and surface any errors immediately.
20. Insert a `projects` row in the Postgres ledger (slug, name, mode, paths, GBrain
    source IDs, `is_active = true`).
21. Self-audit everything above. Surface any errors or inconsistencies immediately. Do
    not correct anything found here without the developer's explicit permission first.
22. Follow the execution sequence in `[[spec-execution-discipline]]`
    — Step Receipt, BFT, and the two end-of-step housekeeping questions, asked here
    regardless of what was decided at items 18–19 — then stop and report. The second
    housekeeping question is now a five-step sequence, not a single sync command:
    (1) commit and push to GitHub; (2) invoke `/mb-submit-memory (path)` for each real,
    developer-written file produced during this step, using the `pdlf_step_sync`
    credential (see item 19's note — this is PDLF's own housekeeping, not an ad-hoc
    request); (3) run `gbrain dream` for real,
    not a dry run — a dry run writes nothing and cannot serve as a check; (4) run
    `gbrain eval suspected-contradictions` immediately afterward; (5) review what that
    command reports, paying real attention to anything marked high-severity.
23. Apply BFT per `[[spec-bft]]` at **Full** — init creates the
    project's architectural foundation.

---

## Description

Runs a single unified procedure for both new and existing project entry. The two modes
differ only in how the two repos are obtained and verified — new entry asks for the code
repo URL and creates the docs repo from scratch; existing entry asks for both URLs and
both local paths, then verifies and corrects the links. Everything from item 15 onward is
identical regardless of entry mode.

No git operation — commit, push, or repo creation — ever runs without the developer's
explicit permission, at any point in this step. This applies even to the early setup
check at items 17–18, which is an early *ask*, not an automatic action; it exists purely
to surface a broken setup immediately rather than at the very end.

## Inputs Required

- New-vs-existing determination (from the developer)
- Project slug (from the developer)
- GitHub code repo URL (from the developer, both entry modes)
- GitHub docs repo URL and both local paths (from the developer, existing entry only)
- Project template at `C:\dev\project-template\dev-(SLUG)\` (new entry only)
- Postgres ledger reachable
- Developer permission for: creating the docs repo (new entry); correcting a broken
  link or missing GBrain registration (existing entry); the early
  `mb-submit-memory` check; the end-of-step five-step housekeeping sequence
  (commit/push, `mb-submit-memory`, `gbrain dream`, `gbrain eval suspected-contradictions`,
  review)

## Outputs

- Local code repo and docs repo folders on disk, linked to GitHub — freshly created and
  templated (new entry) or confirmed and corrected (existing entry)
- `projects` row in the Postgres ledger
- GBrain sources registered for both repos
- GBrain source registered for `project-library-global`, if not already registered
- Updated local `AGENTS.md`, system files, and Matt Pocock skills configuration
- Pre-project files placed in `dev-{slug}\{slug}-project-library\pre-project\`
  (new entry only)
- Step Receipt at `dev-{slug}\{slug}-project-library\pdlf\step-11-receipt.md`
- BFT record — Full

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 11 | Init | | OpenCode |

---

## Handoff

Both entry modes hand off directly to Step 12 ([[[makepdlf-project-library:stepwise/step-12-office-hours|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md)). There is no separate
existing-project audit step — that model is retired. Step 12 itself reads different
source material depending on entry mode: new-project entry works from the three
pre-project files; existing-project entry works from the whole existing project-library.

- **New-project entry:** the three pre-project files are pre-loaded into Step 12's
  prompt.
- **Existing-project entry:** the existing project-library, registered as a GBrain
  source at item 17 above, is what Step 12 reads from.

---

## Reference

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: `[[spec-execution-discipline]]`
For BFT procedure: `[[spec-bft]]`
For the WSL→Windows Postgres bridge pattern: [[[makepdlf-project-library:specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-postgres-ledger.md)

GBrain querying is automatic and read-only. Getting new content into durable memory is a
write action and is never automatic — always asked, at both the early check (items
18–19) and end-of-step housekeeping (item 22). It now goes through the `mb-submit-memory`
skill and the five-step sequence described at item 22, not GStack `/sync-gbrain`.

Git operations (commit, push, repo creation) are permission-only at every point in this
step, per the global [[[makepdlf-project-library:agents|AGENTS.md]]](C:/dev/dev-makepdlf/makepdlf-project-library/AGENTS.md) — never automatic, never run without the
developer's explicit approval first.

The ledger row, Step Receipt, and devlog-index/judgement-trail entries are the complete
checkpoint. No separate state file or completion report.
