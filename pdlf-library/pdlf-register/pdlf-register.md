---
document: "Register — PDLF Library"
doc-id: pdlf-register
state: Live
date-created: 2026-09-11
---

# Register — PDLF Library

One row per real document in `C:\pdlf\pdlf-library\` (and the app-factory
README). `doc-id` is the filename without its `.md` extension. Maintained as
documents land — nothing exists in the library that is not registered here.
Folders `pdlf-policy/`, `pdlf-processes/`, and `pdlf-explainer-docs/pdlf-stepwise/`
hold empty placeholders per the 2026-09-11 deferral ruling (their content is
built in the makePDLF environment and migrates on completion); rows appear
here as their documents land.

| doc-id | filename | folder | type | state | notes |
|---|---|---|---|---|---|
| pdlf-adr-artifact-saving-convention | pdlf-adr/pdlf-adr-artifact-saving-convention.md | pdlf-adr | adr | Live | The 10-decision artifact convention. Closes master-task-list items 18/19. Origin: 2026-06-25 investigation + 2026-09-11 design session. |
| pdlf-spec-artifact-handover | pdlf-specifications/pdlf-spec-artifact-handover.md | pdlf-specifications | spec | Live | Binding handover detail: native save locations, handoff contract, capture-verify-record, stable/safety-net copies, ship-time archival, watched items. Implements the ADR. |
| pdlf-spec-nomenclature | pdlf-specifications/pdlf-spec-nomenclature.md | pdlf-specifications | spec | Live | Naming rules: canonical slug, GStack derivation, the two-GStack-names fact, cache hygiene, copy filenames, folder names per environment. |
| pdlf-expl-orchestrator-agent | pdlf-explainer-docs/pdlf-expl-orchestrator-agent.md | pdlf-explainer-docs | explainer | Live | Step 1's role: the standing agent that runs all steps and administers the standards. Implementation is app-factory Module 1 (to be built). |
| pdlf-expl-artifact-lifecycle | pdlf-explainer-docs/pdlf-expl-artifact-lifecycle.md | pdlf-explainer-docs | explainer | Live | The plain narrative of an artifact's life, born to archived; the June lessons as the "why". |
| pdlf-expl-app-factory | pdlf-explainer-docs/pdlf-expl-app-factory.md | pdlf-explainer-docs | explainer | Live | What the app-factory is; module-per-step; build-once migration; makePDLF archive afterward. |
| pdlf-environment-explainer | pdlf-explainer-docs/pdlf-environment-explainer.md | pdlf-explainer-docs | explainer | Live | The layered-environment orientation doc (pre-makePDLF, makePDLF, PDLF, shipped layers). Moved (not copied) from C:\mybizz\mybizz-os-docs\ by the developer 2026-09-11 — sole home, no duplicate. Note: its internal companion-document references still point at former mybizz-os-docs neighbours — heal in the align-docs pass. |
| pdlf-objective-review | pdlf-explainer-docs/pdlf-objective-review.md | pdlf-explainer-docs | explainer | Live | Moved (not copied) from C:\mybizz\mybizz-os-docs\ by the developer 2026-09-11 — sole home, no duplicate. Content dated 2026-09-05: PDLF assessed against the comparative framework landscape (SDD, BMAD, OpenSpec, Spec Kit, Superpowers, GSD). |
| pdlf-system-explainer | pdlf-explainer-docs/pdlf-system-explainer.md | pdlf-explainer-docs | explainer | Live | Full general PDLF explainer. Moved (not copied) from C:\mybizz\mybizz-os-docs\pdlf-explainer.md by the developer 2026-09-11 — sole home, no duplicate. |
| README | README.md | (library root) | readme | Live | Library purpose, folder map, category tests, naming rules, deferrals, neighbour relationships. |
| app-factory-readme | app-factory/README.md | app-factory (C:\pdlf\app-factory\) | readme | Live | App-factory purpose, module-per-step, migration lifecycle. |
| step-13-readme | pdlf-explainer-docs/pdlf-stepwise/pdlf-step-13/README.md | pdlf-explainer-docs/pdlf-stepwise/pdlf-step-13 | explainer | Live | Reserved-gap note — Step 13 disbanded by design; registered by align-docs 2026-09-17 (relevant, must stay). |

---

*End of pdlf-register*