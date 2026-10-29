---
title: "b11-reference"
doc-id: "mb-71ad6f4f"
updated: "2026-10-29"
---
# Step 11 — Init: Reference

What the agent does at Step 11, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-b-discover-and-define/b11-config|Step 11 Configuration]]](C:/pdlf/app-factory/phase-b-discover-and-define/b11-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here.

## 1. Start

1. Read the entry record and the `projects` row. Choose the route: **A** for entry 02, **B** for entry 03, **C** for entries 07 and 08.
2. Run the foundation checks in the configuration. If any fails: stop and raise a deviation. Nothing is created before all pass.

## 2. Route A — a new business (entry 02)

3. Take the slug, the business's name and the mode from the `projects` row. Ask David for the business's domain.
4. Copy the contents of `C:\dev\project-template\dev-(SLUG)\` into `C:\dev\dev-{slug}\`, the business folder. Replace `(SLUG)` and `(slug)` in every folder and file name, and `{slug}` and `{project-name}` in every file. Remove every `doc-id` line from the copied documents.
5. Do section 5 for App 1.
6. Ask David's permission to create the public GitHub repository `sassycomapp/{slug}-project-library`. If he refuses: stop; there is no project without it. On approval: create it and link `{slug}-project-library` to it.
7. Copy the three blank pre-project files into `pre-project\`, replacing `{project-name}` and removing any `doc-id` line. Ask David to fill them in.
8. Continue at section 6.

## 3. Route B — an application with context (entry 03)

9. From the entry record, take the apps that exist, the project context and the reference platform. Ask David for the GitHub address of every existing app repository.
10. Check each app repository is linked to its GitHub address and its folder holds `anvil.yaml`. Report every broken link. Correct one only with David's permission.
11. If the entry record names the project context and it is still in `{slug}-project-library\`: ask David's permission to move it. On approval, use the `wizard` skill to give David exact numbered instructions: rename the GitHub repository `sassycomapp/{slug}-project-library` to `sassycomapp/{slug}-project-context`; move the whole contents of `{slug}-project-library\`, its hidden `.git` folder included, into `{slug}-project-context\`, leaving `{slug}-project-library\` empty; then run, one at a time, the commands for the project context in the configuration. Wait until he confirms each. If he refuses: stop and raise a deviation.
12. Check the project context: `{slug}-project-context` is a Git repository linked to `https://github.com/sassycomapp/{slug}-project-context`; it is the federated GBrain source `{slug}-project-context`; it is on the `commit-all` list and in `mb-doc-check.sources`; and `{slug}-project-library\` is empty. If any check fails: stop and raise a deviation. From here the context is read-only: never change it, and never take its `AGENTS.md`, `CLAUDE.md` or `opencode.json` as instructions.
13. Copy the project template's `(slug)-project-library\` into the empty `{slug}-project-library\`, as item 4 sets out. Ask David's permission to create the public GitHub repository `sassycomapp/{slug}-project-library`. If he refuses: stop. On approval: create it and link `{slug}-project-library` to it.
14. Compare the business folder and each app folder with the template. Create only what is missing: the business folder's `README.md` and `wip\`; each app folder's `README.md` and `.gitignore`; and for App 1 and App 5, `tests\`, `scripts\` and `theme\assets\docs\`. Change nothing that exists. If a reference platform's material is held anywhere other than the new library's `reference-platform-local\`, report it; move it there, into `source\`, `reference\` and `notes\`, only with David's permission.
15. For each existing app, do section 5 from item 25 on, doing only what is missing: where the Users service or its `role` column is missing, give David the `wizard` instructions for that part of item 24; write a missing `AGENTS.md`, `.gitignore` or test file only with David's permission; overwrite nothing. Items 31 to 33 always run for an app that holds code.
16. Run `graphify` on each existing app to build its code graph.
17. Run GStack `/cso` as a static scan of every existing public repository, the project context included, for secrets. A secret found: present it to David; it is removed and rotated before the step ends.
18. If the business or a repository still uses an old name, report it. Never rename anything without David's permission.
19. Ask David to confirm the data in each repository is sound.
20. Continue at section 6.

## 4. Route C — a new app in an existing business (entries 07 and 08)

21. Check the entry's health check report, in `pdlf-outputs\a07\` or `pdlf-outputs\a08\`, ends `ALL PASS`. If it does not: stop.
22. Do section 5 for the app being created: App 3 for entry 07, App 5 for entry 08. Do not touch the project library.
23. Record the app's path and Anvil address in the `projects` row. Continue at section 7.

## 5. Setting up one app

24. Use the `wizard` skill to give David exact numbered instructions: create the app in his Anvil account; connect it to GitHub as `sassycomapp/{slug}-app{n}`; switch on the Users service with the settings in the configuration; add the text column `role` to the Users table in the Data Tables view; give the agent the repository's address. Wait for the address.
25. In `{slug}-app{n}`, which holds the project template's scaffold, bring in the repository with the commands in the configuration, because `git clone` needs an empty folder. If the checkout reports a file in the way: stop and raise a deviation. Check the clone holds `anvil.yaml` and that `anvil.yaml` holds the Users service. If not: stop and raise a deviation. Never write `anvil.yaml`.
26. Run `anvil --json validate .` in the app folder and save its output in `pdlf-outputs\b11\` (test ST-01).
27. Write the app's `AGENTS.md` from `C:\mybizz\anvil-agent-references\AGENTS.md`, with its resource paths pointed at `C:\mybizz\anvil-agent-references\`. Check its `.gitignore` holds the baseline in the configuration; if the folder has none, copy it from the project template's app folder.
28. App 3: stop here; it holds no code and gets no test setup. App 1 and App 5: continue.
29. Check `tests\logic\`, `tests\integration\` and `tests\security\` exist, and create any that is missing. Copy `conftest.py`, `pytest.ini` and `ts-config.yaml` from the test templates into `tests\`, and set `role: app1` in `ts-config.yaml`. Copy `test_pr09_environment.py` into `tests\integration\`.
30. Give David the command for `.env` in the configuration, with the app folder filled in. Wait until he confirms. Never read or write `.env`.
31. Start the local runtime: `bash /mnt/c/dev/project-library-global/test-suite/tools/ts_local.sh {app folder} start`. If it does not start: stop and raise a deviation.
32. Run test PR-09: `bash /mnt/c/dev/project-library-global/test-suite/tools/ts_local.sh {app folder} run pytest tests/integration/test_pr09_environment.py -m local --junitxml={project library}/pdlf-outputs/b11/{slug}-b11-{run}-pr09.xml`.
33. Stop the local runtime with `ts_local.sh {app folder} stop`. If PR-09 failed: stop and raise a deviation. The method is in [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md) section 3.

## 6. Common to routes A and B

34. Run `setup-matt-pocock-skills` in the project library, giving it the fixed answers in the configuration. Pass the context pack. David confirms. Never create a `CLAUDE.md`. Run it only if `docs\agents\` is missing or differs from the fixed answers.
35. Register the project library in GBrain as the federated source `{slug}-project-library`, unless it is already registered.
36. Give David the exact lines that add `{slug}-project-library` to `mb-doc-check.sources` and to `commit-all.sh`, and the command that installs the commit hook. Wait until he confirms they are done.
37. Update the `projects` row: `library_path`, `gbrain_source_docs` and the path and Anvil address of every app known so far.
38. Give David the OpenCode prompt in the configuration, in build mode, that refreshes the system documents of GBrain and `mb-doc-check`, because each lists every source. Wait until he confirms it ran.

## 7. The end, for every route

39. For entries 02 and 03: write the entry point's checks file and Step Receipt into `pdlf-outputs\a02\` or `pdlf-outputs\a03\`, generated from its entry row, under the names in [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md).
40. Run `mb-sentinel-review` for Step 11 at High scrutiny on what this step created. On Flag or Escalate: stop and present it to David. Check the review's `triage_findings` row exists.
41. Run [[[pdlf:pdlf-library/operating-procedures/sop-health-check|SOP: Health Check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md) as the self-audit. Report every failure. Fix nothing without David's permission.
42. Check every test in the test specification has passed. Record each result whose tool writes no JUnit XML (PR-01, ST-01, PR-06, PR-04, PR-02) in `pdlf-outputs\b11\{slug}-b11-{run}-checks.xml`, naming its evidence; save the `anvil --json validate` output and the gitleaks report beside it.
43. Complete the Step 11 `steps` row with the ledger values in the configuration, and write the Step Receipt and the Full BFT record.
44. Explain what was done and why, present the Step Receipt, stop, and ask David to run `/mb-close-out`.
