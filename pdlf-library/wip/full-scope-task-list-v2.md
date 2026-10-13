---
title: "full-scope-task-list-v2"
updated: "2026-10-13"
doc-id: "mb-0b3dc996"
---
# Full Scope — Deferred Tasks, V2

Tasks found while applying the scope that cannot be finished inside the current section. Each is done as one job.

## Naming and GBrain

1. Replace the old names everywhere they still appear: `mb4ecom`, `mb5pdlf`, the old App 1 path `...\dev-mb-3-cs\mb-3-cs\`, the removed `-code` sources and the `{slug}-app-1` forms. Known places: the `mybizz-os-docs`, `mybizz-config-docs` and `project-library-global` repositories; `~/.config/opencode/AGENTS.md` and the skills `mb-close-out`, `mb-project-docs`, `mb-config-gbrain`, `mb-config-graphify`, `mb-config-opencode` and `mb-config-anvil-agent-references`; `/mnt/c/mybizz/scripts/install-project-docs.py`; each project folder's `README.md`; and `mb4ecom-config.yaml` and `mb5pdlf-config.yaml`, which are also renamed. One tested scripted replacement per repository. (The `pdlf` build plan and `spec-nomenclature.md` are already corrected.)
2. Graphify's settings still point at the old App 1 path: fix them, or remove Graphify.

## Memory governor

3. Check whether the memory governor's project list holds `mb4ecom` or `mb5pdlf`. If so, re-register them as `mb-4-ecom` and `mb-5-pdlf`, because a name that does not match the GBrain source name stops governed facts from arriving.
4. Removing the source `mb-3-cs-code` deleted 2 facts stored in it. Check the memory governor's register and restore them if they were governed.
