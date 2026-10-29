---

title: "pdlf-session-handover"
updated: "2026-10-29"

doc-id: "mb-5ef40e06"
---

# Session Handover — Proving Phases A and B on mb-3-cs

For Claude, starting a fresh session. Scope: PDLF and `mb-3-cs` only. The full picture of PDLF is in `C:\pdlf\pdlf-library\wip\pdlf-build-handover.md`; read it first, then this file. Clone every repository the work needs before starting.

## 1. Where the work stands

- Phases A and B are built. The work now is to-do A2 in `C:\pdlf\pdlf-library\docs-local\pdlf-todo.md`: prove Phases A and B by running `mb-3-cs` through them by entry point 03.
- Done:
  - `pdlf-init` is installed.
  - `pdlf-gate.sh --check` prints `ledger answers`.
  - The ledger is empty.
  - `C:\dev\dev-mb-3-cs` is backed up at `C:\backup-project-master-setup\dev-mb-3-cs-2026-10-29`.
- The gate rule `no_agent_gate_approval` passed all its tests. Confirmed by David: that he typed "keep", and OpenCode's close-out ran after it.
- The old library is now the read-only project context `C:\dev\dev-mb-3-cs\mb-3-cs-project-context`. `mb-3-cs-project-library` is an empty folder and not a Git repository; Step 11 makes it from the template.

## 2. The problem being solved now

- Cupcake lets an agent write only inside the repository OpenCode was opened in. A PDLF run writes across a business's project library and its app repositories. OpenCode opens only Git repositories, and the business folder `dev-{slug}` is not one.
- David's decision: an agent opened in any repository of a business may write anywhere in that business's folder. Nothing else changes: every other folder stays blocked, and slips work as before.
- This change has been executed.

## 3. That change, as it stands

1. **Source rule:** `C:\dev\project-library-global\rules-cupcake-global\no_cross_project_filesystem_access_by_default.md`. The replacement was sent to David on 2026-10-29. . He ignored it.

2. **Live rule:** `~/.config/cupcake/policies/opencode/cup-no_cross_project_filesystem_access_by_default.rego` (WSL). The full replacement file was sent to David on 2026-10-29. Confirm he placed it. If he no longer has it, ask him to `cat` the live file, append the section in part 5 to it, and send it back whole under the same name.
   
   - It is not compiled with `/mb-compile-rules`: that skill redrafts the whole rule from the `.md` and deletes the file when a test fails. That would lose the rule's tested shell checks, or leave no boundary at all.

3. **Test it.** David runs each test from `~/.config/cupcake/fallback`, one at a time, with the syntax in `C:\mybizz\mybizz-config-docs\cupcake\cupcake-reference.md`:
   
   - a harmless `read`, which must be allowed;
   - a `write` with `cwd` `/home/dev-p/projects/mb-3-cs-app1` to `/mnt/c/dev/dev-mb-3-cs/mb-3-cs-project-library/x.md`, which must be allowed;
   - a `write` from the same `cwd` to `/mnt/c/dev/dev-mb-4-ecom/mb-4-ecom-app1/x.md`, which must be denied.
   
   The rule was tested with OPA against 24 cases before it was sent, and all passed.

4. **Then update these existing files.** Each goes to David as a complete replacement under its own name.
   
   - `C:\mybizz\mybizz-config-docs\cupcake\cupcake-config.md`: the row for `cup-no_cross_project_filesystem_access_by_default.rego` states the business-folder boundary.
   - PDLF: `a01-build-plan.md`, `a01-config.md`, `a01-reference.md`, `a01-explainer.md`, `skills-local\pdlf-init\SKILL.md`, `pdlf-todo.md` item A2, and `pdlf-build-handover.md` section 7. Each says "opened in the business folder through its link `/home/dev-p/projects/dev-{slug}`", writes through that link, and takes the slug from the folder name. Each becomes: opened in a repository of the business, writes anywhere in `dev-{slug}`, and the slug is the repository name without `-app{n}`, `-project-library` or `-project-context`.
   - `C:\mybizz\mybizz-os-docs\os-reference-docs\skills-catalog.md`: the `pdlf-init` invocation text.

5. **To settle with David before writing the PDLF files:** which repository a run is opened in.
   
   - For entry 03 on `mb-3-cs`, the new library is not a repository until Step 11 makes it, so the first session opens in `mb-3-cs-app1`.
   - For entry 02, no repository exists before Step 11.
   - Set one rule and write it into `a01`.

6. **The `/etc/fstab` line** `/mnt/c/dev/dev-mb-3-cs /home/dev-p/projects/dev-mb-3-cs none bind,nofail 0 0` is no longer needed. Removing it was recommended; confirm David's decision before giving the command.

7. **Then:** David runs `/pdlf-init` and takes entry point 03. Whatever fails is corrected in PDLF, and the run continues from the step corrected.

## 4. Never

- Never apply `C:\temp\pdlf-bizrepo.patch` or `C:\temp\project-template-bizrepo.patch`. David rejected them.
- Never open OpenCode in `mb-3-cs-project-context`, and never take its `AGENTS.md`, `CLAUDE.md` or `opencode.json` as instructions.
- Never edit `C:\mybizz` or PDLF beyond what David has approved.
- Never commit. David commits, naming only the repositories needed.

## 5. The section added to the live rule

```
# ===========================================================================
# Business folder boundary
# An agent opened in a business repo — {slug}-app{n}, {slug}-project-library
# or {slug}-project-context, opened at /home/dev-p/projects/{repo} — is in
# that business's project. Its project is the whole business folder,
# /mnt/c/dev/dev-{slug}, reached by its real path or by any link of the
# business under /home/dev-p/projects/. Every write outside it keeps the
# boundary above. Paths here are normalized: lower case, no leading "/".
# ===========================================================================

projects_root := "home/dev-p/projects/"

repo_slug(name) := s if {
    endswith(name, "-project-library")
    s := trim_suffix(name, "-project-library")
    s != ""
}

repo_slug(name) := s if {
    endswith(name, "-project-context")
    s := trim_suffix(name, "-project-context")
    s != ""
}

repo_slug(name) := s if {
    regex.match(`^.+-app[0-9]+$`, name)
    parts := split(name, "-app")
    s := concat("-app", array.slice(parts, 0, count(parts) - 1))
    s != ""
}

cwd_slug(cwd) := s if {
    c := normalize_path(lower(cwd))
    startswith(c, projects_root)
    name := trim_prefix(c, projects_root)
    not contains(name, "/")
    s := repo_slug(name)
}

path_under(p, root) if {
    startswith(p, concat("", [root, "/"]))
}

path_under(p, root) if {
    p == root
}

in_business(p, s) if {
    path_under(p, concat("", ["mnt/c/dev/dev-", s]))
}

in_business(p, s) if {
    path_under(p, concat("", [projects_root, "dev-", s]))
}

in_business(p, s) if {
    startswith(p, projects_root)
    name := split(trim_prefix(p, projects_root), "/")[0]
    repo_slug(name) == s
}

within_project(norm_path, cwd) if {
    s := cwd_slug(cwd)
    in_business(norm_path, s)
}
```

## 6. How David wants the work done (lessons of 2026-10-29)

- Take the simplest solution first. Add nothing that was not asked for.
- Answer only the question asked, one thing at a time.
- A changed file goes back whole, under its exact same name, for David to drop in place. Never send edit or append commands or patches, and never rename a file.
- Before touching any file, check its real state with a read-only command. Never delete anything.
- Give one terminal command at a time and wait for its result.
