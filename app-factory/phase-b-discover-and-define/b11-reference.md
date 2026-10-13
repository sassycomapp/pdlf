---
title: "b11-reference"
doc-id: "mb-71ad6f4f"
updated: "2026-10-13"
---
# Step 11 — Init: Reference

What the agent does at Step 11, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-b-discover-and-define/b11-config|Step 11 Configuration]]](C:/pdlf/app-factory/phase-b-discover-and-define/b11-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here.

## 1. Start

1. Read the entry record. Choose the route: **A** for entry 02, **B** for entry 03, **C** for entries 07 and 08.
2. Run the foundation checks in the configuration. If any fails: stop and raise a deviation. Nothing is created before all pass.

## 2. Route A — a new business (entry 02)

3. Ask David for the slug (the business's short name, lowercase, hyphens kept), the business's name, its domain and the mode (`full` or `test`).
4. Copy `C:\dev\project-template\dev-(SLUG)\` to `C:\dev\dev-{slug}\`. Replace `(SLUG)` and `(slug)` in every folder and file name, and `{slug}` and `{project-name}` in every file. Remove every `doc-id` line from the copied documents.
5. App 1. Use the `wizard` skill to give David exact numbered instructions: create the app in his Anvil account, connect it to GitHub as `sassycomapp/{slug}-app1`, and give the agent its address. Wait for the address.
6. Remove `{slug}-app1\.gitkeep`, then clone the address into `{slug}-app1`. Check the clone holds `anvil.yaml`. If not: stop and raise a deviation. Never write `anvil.yaml`.
7. Write App 1's `AGENTS.md` from `C:\mybizz\anvil-agent-references\AGENTS.md`, with its resource paths pointed at `C:\mybizz\anvil-agent-references\`. Write its `.gitignore` from the baseline in the configuration.
8. Ask David's permission to create the private GitHub repository `sassycomapp/{slug}-project-library`. If he refuses: stop; there is no project without it. On approval: create it and link `{slug}-project-library` to it.
9. Copy the three blank pre-project files into `pre-project\`, replacing `{project-name}` and removing any `doc-id` line. Ask David to fill them in.
10. Continue at section 5.

## 3. Route B — an application with context (entry 03)

11. Ask David for the GitHub address and local path of every repository the business has: each app that exists and the project library.
12. Check each repository is linked to its GitHub address, and each app folder holds `anvil.yaml`. Report every broken link. Correct one only with David's permission.
13. Compare the business folder and the project library with the template. Create only folders that are missing, including any missing `pdlf-outputs\` step folder and `pdlf-tickets\`. Change nothing that exists.
14. For each app folder without an `AGENTS.md` or `.gitignore`, propose them as in item 7, and write them only with David's permission.
15. If the business or a repository still uses an old name, report it. Never rename anything.
16. Ask David to confirm the data in each repository is sound.
17. Continue at section 5.

## 4. Route C — a new app in an existing business (entries 07 and 08)

18. Run [[[pdlf:pdlf-library/operating-procedures/sop-health-check|SOP: Health Check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md) on the business. If any check fails: stop.
19. For the app being created (App 3 for entry 07, App 5 for entry 08), do items 5 to 7 with that app's number.
20. Record the app's path and Anvil address in the `projects` row. Do not touch the project library.
21. Continue at item 26.

## 5. Common to routes A and B

22. Run `setup-matt-pocock-skills` in the project library, giving it the fixed answers in the configuration. Pass the context pack. David confirms. Never create a `CLAUDE.md`. In route B, run it only if `docs\agents\` is missing or differs from the fixed answers.
23. Register the project library in GBrain as the federated source `{slug}-project-library`, unless it is already registered.
24. Give David the exact lines that add `{slug}-project-library` to `mb-doc-check.sources` and to `commit-all.sh`, and the command that installs the commit hook. Wait until he confirms they are done.
25. Write or update the `projects` row: slug, name, mode, `library_path`, `gbrain_source_docs` and the path and Anvil address of every app known so far.

## 6. The end, for every route

26. Run `mb-sentinel-review` for Step 11 at High scrutiny on what this step created. On Flag or Escalate: stop and present it to David. Check the review's `triage_findings` row exists.
27. Run [[[pdlf:pdlf-library/operating-procedures/sop-health-check|SOP: Health Check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md) as the self-audit. Report every failure. Fix nothing without David's permission.
28. Write the Step 11 `steps` row with the ledger values in the configuration, the Step Receipt and the Full BFT record.
29. Explain what was done and why, present the Step Receipt, stop, and ask David to run `/mb-close-out`.
