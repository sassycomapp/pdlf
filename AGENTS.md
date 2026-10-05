---
title: "AGENTS"
doc-id: "mb-a65c6e3a"
updated: "2026-10-05"
---
# AGENTS.md — pdlf (the PDLF environment)

**What this location is.** `C:\pdlf` is the home of the PDLF system — the
Project Development Lifecycle Framework: the harness through which Anvil
applications get built, step by step, with gates, reviews, QA, and
verification. The system is being developed in the makePDLF environment
(`C:\dev\dev-makepdlf\makepdlf-project-library`); this location holds the
system itself — its documentation library, its machinery scaffold, and its
artifact safety net.

## Structure

| Path | What it is |
|---|---|
| `pdlf-library\` | The PDLF library — canonical technical documentation: ADRs, specifications, policies, processes, explainers. See `pdlf-library\README.md`. |
| `app-factory\` | The system's machinery — 46 modules, one per pipeline step. Placeholders today; populated by makePDLF and migrated here once, when all steps are complete. See `app-factory\README.md`. |
| `output\` | The artifact safety net — producer-routed local copies (`pdlf-output-gstack\`, `pdlf-output-pocock\`). Transient: copied into the shipping project's folders, then cleared. Not version-controlled. |

## Standing rules for this location

1. **The machinery is built in makePDLF and migrated here once**, when all
   46 steps are complete. Do not build or edit app-factory modules here
   before migration; do not develop PDLF components here.
2. **Library documents that are settled and canonical to the PDLF system are
   written directly into `pdlf-library\`.** Stepwise explainers, the gating
   policy, and the closeout process stay in makePDLF until the steps are
   done, then migrate with the modules.
3. **The output area serves exactly one project at a time** — the one in
   PDLF's pipeline. Ship-time rule: copy into the project's folders first,
   verify, then clear. Convention: `pdlf-adr-artifact-saving-convention.md`.
4. **While makePDLF is being built, makePDLF's own runs save their outputs
   in the makePDLF environment** (the chicken-and-egg exception) — not here.
5. Nothing runs in this location yet: the machinery arrives with the
   app-factory migration. No PDLF step-work happens here until then.

## History (kept short)

An earlier, abandoned first attempt at building PDLF directly in this
location was deleted outright on 2026-08-13 (explicit developer decision —
superseded content with no future use). A `.git` folder pointing at
`sassycomapp/pdlf` existed until 2026-09-05, when the by-then-deleted GitHub
repo left it orphaned and it was removed by explicit developer decision. The
environment was scaffolded properly on 2026-09-11 per developer instruction:
the library, the app-factory placeholders, the output
area, and the re-established GitHub repository.