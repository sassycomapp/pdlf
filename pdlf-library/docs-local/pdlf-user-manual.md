---
title: "pdlf-user-manual"
updated: "2026-10-29"
doc-id: "mb-6ea8e798"
---
# PDLF User Manual

How to operate PDLF, step by step. Each step says where it happens: **WSL terminal**, **OpenCode** or **Claude**.

## 1. Before a run

### A new business (once)

1. **WSL terminal:** create the business folder and its App 1 folder, and make App 1 a Git repository:
   `mkdir -p /mnt/c/dev/dev-{slug}/{slug}-app1 && git -C /mnt/c/dev/dev-{slug}/{slug}-app1 init`
2. **Claude:** ask for the command that adds App 1's link to `/etc/fstab`. Run it in the WSL terminal.
3. **WSL terminal:** check the link is connected:
   `mountpoint /home/dev-p/projects/{slug}-app1`
   It must print `is a mountpoint`.

### An existing business

1. App 1 already exists at `C:\dev\dev-{slug}\{slug}-app1` with its link `projects/{slug}-app1`. Nothing to do.

### Every run

1. **Windows:** back up the whole business folder, `C:\dev\dev-{slug}\`, to `C:\backup-project-master-setup\dev-{slug}-{yyyy-mm-dd}`.

## 2. Start a session

1. **WSL terminal:** `cd ~ && opencode web --hostname 0.0.0.0`
2. **OpenCode:** in the project picker, open `projects/{slug}-app1`. Always App 1, for every run of every business.
3. **OpenCode:** select the **Build** agent.
4. **OpenCode:** type `/pdlf-init`

## 3. Start or continue a run

1. If the business has an unfinished run, the orchestrator offers to continue it where it stopped. Choose it to continue.
2. Otherwise, choose one entry point:

| Your situation | Entry |
|---|---|
| A new business with no material yet | 02 |
| A business with existing material, never run through PDLF (e.g. `mb-3-cs`) | 03 |
| A new feature in App 1 | 04 |
| A change to App 1 | 05 |
| Release App 1 into App 2 | 06 |
| Create App 3, the client template | 07 |
| Create App 5, the management app | 08 |
| A new feature in App 3 or App 5 | 09 |
| A change to App 3 or App 5 | 10 |

3. Answer the orchestrator's questions. For 02 and 03 it asks the business's name and the mode (`full` or `test`).

## 4. During the run

1. The agent stops at every step. Read what it reports and answer it.
2. **A gate:** the agent stops and asks you to approve it. Approve it yourself:
   **WSL terminal:** `bash /mnt/c/mybizz/scripts/pdlf-gate.sh {slug} {gate} {run}`
   Then tell the agent to continue. The agent can never approve a gate.
3. **A deviation:** the agent sets out options. You decide. Ask Claude for the recommended option if unsure.
4. **Your own actions.** The agent gives exact instructions; you carry them out, then tell it you are done:
   - create an app in Anvil and connect it to GitHub as `{slug}-app{n}`;
   - switch on the app's Users service and add its `role` column;
   - write the app's `.env` with the command the agent gives;
   - apply a schema change in Anvil's Data Tables view.
5. **A permission slip:** if the agent needs to write outside its business, it stops and gives you an `mg-grant` line. Run it in the WSL terminal only if you agree, then tell the agent to continue.
6. **Something fails:** stop the run and bring the failure to Claude. The failure is corrected in PDLF, and the run continues from the step corrected.

## 5. End a session

1. **OpenCode:** run `/mb-close-out`.
2. **Claude:** ask for the commit command. Run it in the WSL terminal. Only you commit; the agent never does.

## 6. Never

- Never open `{slug}-app2` or `{slug}-project-context` in OpenCode.
- Never open `projects/pdlf` for a run. PDLF is only read during a run.
- Never let the agent write `.env` or `anvil.yaml`.
- Never start a run without the backup.
