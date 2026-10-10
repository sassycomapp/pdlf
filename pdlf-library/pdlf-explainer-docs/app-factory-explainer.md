---
title: "pdlf-expl-app-factory"
doc-id: "mb-bcfa10bb"
updated: "2026-10-10"
---
# PDLF — The App Factory

*What the app-factory is: the actual machinery of the PDLF system, one module
per step.*

---

## What it is

The app-factory (`C:\pdlf\app-factory\`) holds the executable machinery of
the PDLF system: forty-six modules, `module-1.md` through `module-46.md`,
mirroring the forty-six pipeline steps one-to-one. Each module holds exactly
the output that the makePDLF development project produces for its
corresponding step — a skill, or a module that defines and runs that
particular step. When the PDLF system runs a project, these modules are the
things that actually run.

The numbering is deliberate and mirrors the steps, including the permanent
gaps (Steps 13 and 25 were disbanded; their numbers are reserved gaps, not
omissions).

## Where the modules come from

They are **built in the makePDLF environment and migrated once.** The
makePDLF development project (`C:\dev\dev-makepdlf\makepdlf-project-library`)
exists to produce this machinery, one module per step, as each step is
completed. Modules are not copied into the PDLF environment piecemeal: they
are migrated into `C:\pdlf\app-factory\` once, when all 46 steps are
complete. This build-once migration is deliberate — retrofitting changes
into partially migrated modules would mean decompiling, changing, and
recompiling, a mission with no upside. While development continues, the
makePDLF environment is the single place where step machinery lives and
changes.

When migration is done, the makePDLF environment is wrapped up and archived
as a completed project. What remains is the PDLF system: the app-factory
machinery, this library's documentation, and the output area, all under
`C:\pdlf\`.

## What the modules must implement

Every module implements the conventions recorded in this library — above
all, for its own step, [[[pdlf:pdlf-library/specifications-local/spec-artifact-handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md): paste prior
artifacts in full, capture the output path, verify it exists, record it in
the ledger, make the stable and safety-net copies, and stop with a deviation
request when something expected is missing. The convention ADR
([[[pdlf:pdlf-library/adr-local/artifact-saving-convention]]](C:/pdlf/pdlf-library/adr-local/artifact-saving-convention.md)) is the decision record behind
those rules.

Module 1 is a special case: it is the orchestrator machinery itself — the
standing agent that runs every other module (see
[[[pdlf:pdlf-library/pdlf-explainer-docs/orchestrator-agent-explainer]]](C:/pdlf/pdlf-library/pdlf-explainer-docs/orchestrator-agent-explainer.md)).

## Current state

All forty-six module files are placeholders, created 2026-09-11 as part of
the PDLF environment scaffold. They are populated as makePDLF completes each
step — not before, and not in bulk.

---

*End of pdlf-expl-app-factory*