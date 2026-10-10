---
title: "project-library-global-registration"
doc-id: "mb-445b1f4d"
updated: "2026-10-10"
---
# ADR — project-library-global Becomes a Registered Foundational Component

**Status:** Accepted

**Date:** [current session]

---

## Context

`project-library-global` holds the shared standards, specifications, and ADRs that apply
across every Anvil.works project PDLF builds. It existed only as a local, unregistered
folder — no remote repo, no GBrain registration. This meant it had none of the integrity
or continuity guarantees already given to every per-project repo (`{slug}`,
`{slug}-project-library`), and no queryable presence an agent could actually search
against when checking a project's decisions for conflicts with the global standard.

## Decision

`project-library-global` becomes a real git repository with a remote, registered as a
GBrain source — done once, ever, not per-project. It is part of a foundational system
layer that exists independently of, and prior to, any single project's PDLF run:
OpenCode, GStack, GBrain, the Magdoub wireframe skill, and `project-library-global`
together.

`project-library-global` is the only source of standards and specifications for any
project PDLF builds. Where a step's output touches a domain with a corresponding global
specification, that specification governs. Local project content that conflicts with it
is resolved in favor of the global standard by default, subject to a deviation request to
the developer where there's a real reason to diverge — reusing PDLF's existing
deviation-request mechanism, not a new one.

If PDLF needs a standard during a project's development that isn't yet in
`project-library-global`, and it isn't canonical to just that one project, the answer is
not to write it locally. The developer is asked to add it to the global library, and PDLF
proceeds once GBrain reflects the update.

## Consequences

- Every GBrain query made during a project's run must explicitly nominate
    `project-library-global` as one of its scoped sources, alongside `{slug}` and
    `{slug}-project-library` — see the updated [[[pdlf:pdlf-library/policy-local/pol-memory-and-knowledge|Policy: Memory and Knowledge]]](C:/pdlf/pdlf-library/policy-local/pol-memory-and-knowledge.md).
- Local/global conflict-checking becomes possible at Steps 14 and 15 (CEO review, Eng
  review) — see [[[pdlf:stepwise/step-14-build-notes|Step 14 Build Notes]]](C:/pdlf/stepwise/step-14-build-notes.md) and
  [[[pdlf:stepwise/step-15-build-notes|Step 15 Build Notes]]](C:/pdlf/stepwise/step-15-build-notes.md).
- This applies to existing-project entry too: an old project-library brought into PDLF
  for redevelopment may contain years of decisions made before this rule existed. Nothing
  here makes that retroactively non-compliant — the check applies going forward, from
  Steps 14/15 onward, not backward into history that predates it.
- **Open, not yet decided:** exactly where PDLF verifies this foundational layer is in
  place. Two options on the table — inside Step 11 as an additional foundation check
  (alongside the existing Postgres-reachability check), or as a separate one-time
  bootstrap procedure that runs outside the numbered step sequence entirely, before any
  project run starts. Needs a decision before this ADR's implementation is complete.
