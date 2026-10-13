---

title: "phase-b-scope-task-list-v1"
updated: "2026-10-13"

doc-id: "mb-6be10f35"
---

# Phase B Scope — Deferred Tasks, V1

Tasks found while remediating the Phase B scope that cannot be finished inside the scope document itself. Each is done as one job, outside the section remediation.

## Naming and GBrain

1. Add the rule "no application code as GBrain sources" to the PDLF build plan and the relevant explainers.
2. Correct the build plan's project scaffold (section 1) to the names `{slug}-app1`, `{slug}-app2`, `{slug}-app3`, `{slug}-app5` and `{slug}-project-library`, and remove its "no hyphens" rule and the `mb3cs` rename line.
3. Replace the old names everywhere they still appear: `mb4ecom`, `mb5pdlf`, the old App 1 path `...\dev-mb-3-cs\mb-3-cs\`, the removed `-code` sources and the `{slug}-app-1` forms. Known places: the `pdlf`, `mybizz-os-docs`, `mybizz-config-docs` and `project-library-global` repositories; `~/.config/opencode/AGENTS.md` and the skills `mb-close-out`, `mb-project-docs`, `mb-config-gbrain`, `mb-config-graphify`, `mb-config-opencode` and `mb-config-anvil-agent-references`; `/mnt/c/mybizz/scripts/install-project-docs.py`; each project folder's `README.md`; and `mb4ecom-config.yaml` and `mb5pdlf-config.yaml`, which are also renamed. One tested scripted replacement per repository.
4. Graphify's settings still point at the old App 1 path: fix them

## Memory governor

5. Check whether the memory governor's project list holds `mb4ecom` or `mb5pdlf`. If so, re-register them as `mb-4-ecom` and `mb-5-pdlf`, because a name that does not match the GBrain source name stops governed facts from arriving.
6. Removing the source `mb-3-cs-code` deleted 2 facts stored in it. Check the memory governor's register and restore them if they were governed.
