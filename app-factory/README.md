---
document: "App Factory — PDLF Machinery"
doc-id: app-factory-readme
state: Live
date-created: 2026-09-11
---

# App Factory — PDLF Machinery

The executable machinery of the PDLF system: forty-six modules, one per
pipeline step, `module-1.md` through `module-46.md`. Each module holds the
output the makePDLF development project produces for its corresponding step —
a skill, or a module that defines and runs that step.

- **Built in makePDLF, migrated once.** Modules are populated as makePDLF
  completes each step, and migrate into this folder only when all 46 are
  complete. Until then, the live machinery lives in the makePDLF environment.
- **Modules implement the conventions** in `C:\pdlf\pdlf-library\` — above
  all `C:\pdlf\pdlf-library\pdlf-specifications\pdlf-spec-artifact-handover.md` and
  `C:\pdlf\pdlf-library\pdlf-adr\pdlf-adr-artifact-saving-convention.md`.
- **Module 1** is the orchestrator machinery — the standing agent that runs
  every other module (see `pdlf-library/pdlf-explainer-docs/pdlf-expl-orchestrator-agent.md`).
- Steps 13 and 25 are reserved gaps: those steps were disbanded; their numbers
  are kept empty by design.
- Current state: all module files are placeholders (created 2026-09-11),
  populated step by step as makePDLF completes them. What it is and why it is
  built this way: `pdlf-library/pdlf-explainer-docs/pdlf-expl-app-factory.md`.

---

*End of README — App Factory*