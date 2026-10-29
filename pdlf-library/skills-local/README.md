---
title: "README"
doc-id: "mb-1e7a8e2e"
updated: "2026-10-29"
---
# skills-local

PDLF's own OpenCode skills, one folder per skill, each holding its `SKILL.md`. A skill here is the source; OpenCode loads the installed copy at `~/.config/opencode/skills/{skill}/SKILL.md`, which David makes with one `cp` command whenever the source changes. The commit hook never touches a `SKILL.md` file, so its frontmatter stays in OpenCode's form (`name`, `description`) and its paths are written plainly.

| Skill | What it does | Used at |
|---|---|---|
| `pdlf-init` | Starts the orchestrator, Step 1: resumes an unfinished run or takes a new entry point, then runs the run's steps | Step 1 |

Every skill is registered in `C:\mybizz\mybizz-os-docs\os-reference-docs\skills-catalog.md`, with the PDLF steps that use it.
