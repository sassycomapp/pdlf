---
title: "b11-reference"
doc-id: "mb-71ad6f4f"
updated: "2026-10-24"
---
# Step 11 — Init: Reference

What the agent does at Step 11, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-b-discover-and-define/b11-config|Step 11 Configuration]]](C:/pdlf/app-factory/phase-b-discover-and-define/b11-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here.

## 1. Start

1. Read the entry record. Choose the route: **A** for entry 02, **B** for entry 03, **C** for entries 07 and 08.
2. Run the foundation checks in the configuration. If any fails: stop and raise a deviation. Nothing is created before all pass.

## 2. Route A — a new business (entry 02)

3. Ask David for the slug (the business's short name, lowercase, hyphens kept), the business's name, its domain and the mode (`full` or `test`).
4. Copy `C:\dev\project-template\dev-(SLUG)\` to `C:\dev\dev-{slug}\`. Replace `(SLUG)` and `(slug)` in every folder and file name, and `{slug}` and `{project-name}` in every file. Remove every `doc-id` line from the copied documents.
5. Do section 5 for App 1.
6. Ask David's permission to create the public GitHub repository `sassycomapp/{slug}-project-library`. If he refuses: stop; there is no project without it. On approval: create it and link `{slug}-project-library` to it.
7. Copy the three blank pre-project files into `pre-project\`, replacing `{project-name}` and removing any `doc-id` line. Ask David to fill them in.
8. Continue at section 6.

## 3. Route B — an application with context (entry 03)

9. Ask David for the GitHub address and local path of every repository the business has: each app that exists and the project library.
10. Check each repository is linked to its GitHub address, and each app folder holds `anvil.yaml`. Report every broken link. Correct one only with David's permission.
11. Compare the business folder and the project library with the template. Create only what is missing, including any missing `pdlf-outputs\` step folder and `pdlf-tickets\`. Change nothing that exists.
12. For each existing app, do section 5 from item 22 on, doing only what is missing: where the Users service or its `role` column is missing, give David the `wizard` instructions for that part of item 21; write a missing `AGENTS.md`, `.gitignore` or test file only with David's permission; overwrite nothing. Items 28 to 30 always run for an app that holds code.
13. Run `graphify` on each existing app to build its code graph.
14. Run GStack `/cso` as a static scan of every existing public repository for secrets. A secret found: present it to David; it is removed and rotated before the step ends.
15. If the business or a repository still uses an old name, report it. Never rename anything.
16. Ask David to confirm the data in each repository is sound.
17. Continue at section 6.

## 4. Route C — a new app in an existing business (entries 07 and 08)

18. Run [[[pdlf:pdlf-library/operating-procedures/sop-health-check|SOP: Health Check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md) on the business. If any check fails: stop.
19. Do section 5 for the app being created: App 3 for entry 07, App 5 for entry 08. Do not touch the project library.
20. Record the app's path and Anvil address in the `projects` row. Continue at section 7.

## 5. Setting up one app

21. Use the `wizard` skill to give David exact numbered instructions: create the app in his Anvil account; connect it to GitHub as `sassycomapp/{slug}-app{n}`; switch on the Users service with the settings in the configuration; add the text column `role` to the Users table in the Data Tables view; give the agent the repository's address. Wait for the address.
22. Remove `{slug}-app{n}\.gitkeep`, then clone the address into `{slug}-app{n}`. Check the clone holds `anvil.yaml` and that `anvil.yaml` holds the Users service. If not: stop and raise a deviation. Never write `anvil.yaml`.
23. Run `anvil --json validate .` in the app folder and save its output in `pdlf-outputs\b11\` (test ST-01).
24. Write the app's `AGENTS.md` from `C:\mybizz\anvil-agent-references\AGENTS.md`, with its resource paths pointed at `C:\mybizz\anvil-agent-references\`. Write its `.gitignore` from the baseline in the configuration.
25. App 3: stop here; it holds no code and gets no test setup. App 1 and App 5: continue.
26. Create `tests\logic\`, `tests\integration\` and `tests\security\`. Copy `conftest.py`, `pytest.ini` and `ts-config.yaml` from the test templates into `tests\`, and set `role: app1` in `ts-config.yaml`. Copy `test_pr09_environment.py` into `tests\integration\`.
27. Give David the command for `.env` in the configuration, with the app folder filled in. Wait until he confirms. Never read or write `.env`.
28. Start the local runtime: `bash /mnt/c/dev/project-library-global/test-suite/tools/ts_local.sh {app folder} start`. If it does not start: stop and raise a deviation.
29. Run test PR-09: `bash /mnt/c/dev/project-library-global/test-suite/tools/ts_local.sh {app folder} run pytest tests/integration/test_pr09_environment.py -m local --junitxml={project library}/pdlf-outputs/b11/{slug}-b11-{run}-pr09.xml`.
30. Stop the local runtime with `ts_local.sh {app folder} stop`. If PR-09 failed: stop and raise a deviation. The method is in [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md) section 3.

## 6. Common to routes A and B

31. Run `setup-matt-pocock-skills` in the project library, giving it the fixed answers in the configuration. Pass the context pack. David confirms. Never create a `CLAUDE.md`. In route B, run it only if `docs\agents\` is missing or differs from the fixed answers.
32. Register the project library in GBrain as the federated source `{slug}-project-library`, unless it is already registered.
33. Give David the exact lines that add `{slug}-project-library` to `mb-doc-check.sources` and to `commit-all.sh`, and the command that installs the commit hook. Wait until he confirms they are done.
34. Write or update the `projects` row: slug, name, mode, `library_path`, `gbrain_source_docs` and the path and Anvil address of every app known so far.

## 7. The end, for every route

35. Run `mb-sentinel-review` for Step 11 at High scrutiny on what this step created. On Flag or Escalate: stop and present it to David. Check the review's `triage_findings` row exists.
36. Run [[[pdlf:pdlf-library/operating-procedures/sop-health-check|SOP: Health Check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md) as the self-audit. Report every failure. Fix nothing without David's permission.
37. Check every test in the test specification has passed. Record each result whose tool writes no JUnit XML (PR-01, ST-01, PR-06, PR-04, PR-02) in `pdlf-outputs\b11\{slug}-b11-{run}-checks.xml`, naming its evidence; save the `anvil --json validate` output and the gitleaks report beside it.
38. Write the Step 11 `steps` row with the ledger values in the configuration, the Step Receipt and the Full BFT record.
39. Explain what was done and why, present the Step Receipt, stop, and ask David to run `/mb-close-out`.
