---
title: "pdlf-phase-b-docs-handover"
updated: "2026-10-22"
doc-id: "mb-cb08abdc"
---
# Handover — Phase B Step Documents

## 1. The job

Bring the Phase B step documents of the app factory up to date, one step (suite) at a time, in this order: `b11`, `b12`, `b14`, `b15`, `b16`. `b13` is a placeholder (Step 13 is not used) and needs no work.

For each step, five documents are in scope:

| Document | File | Work |
|---|---|---|
| Build plan | `{step}-build-plan.md` | Close it: settle every gathered section, leave only the step entry and "Why it is built this way" |
| Config | `{step}-config.md` | Write from the closed build plan |
| Reference | `{step}-reference.md` | Write from the closed build plan |
| Explainer | `{step}-explainer.md` | Write from the closed build plan |
| Decision tree | `{step}-decision-tree.html` | Generate from the reference |

Out of scope: `{step}-test-spec.md` (finished on 2026-10-22; it is the authority on testing, see section 5) and `{step}-module.md` (compiled last, only after the phase has run on `mb-5-pdlf`).

All files are in `C:\pdlf\app-factory\phase-b-discover-and-define\` (repository `sassycomapp/pdlf`).

## 2. The method to follow

The method is `C:\pdlf\pdlf-library\docs-local\app-factory-docs-update-method.md`. Read it first. In short, per step:

1. Close the build plan.
2. Check the test spec against the closed build plan (read-only this time: the test spec is finished; if the build plan and the test spec disagree, the build plan is corrected, see section 5).
3. Write the config: fixed values only (identity, inputs, outputs, file paths, skills, gate, BFT level, Sentinel scrutiny, test spec).
4. Write the reference: what the agent does, in order.
5. Write the explainer: what the step is, how it works, why, what has to happen.
6. Generate the decision tree from the reference.
7. Send the files, each with the path of the file it replaces.

A fact lives in only one of config, reference and explainer.

Two corrections to make in the method document itself, in the first batch of files:
- Its last bullet says testing "is added when designed" and steps "carry the light testing element". The test suite now exists (section 5): replace that bullet with "Each step's testing is its `{step}-test-spec.md`, drawn from the test suite in `C:\dev\project-library-global\test-suite\`."
- Step 2 says "Correct it where the build plan changed". It stays, but the test spec is now the reference for what the step must produce for testing.

## 3. The model of a finished suite

`b11` was written on 2026-10-13 and is the model:
- `b11-build-plan.md`: only "## Step entry" (Must achieve, Starts from, Produces, Carried out by, Must be built so that, BFT level, References, Skills, Layers with no skill, Testing, Standards) and "## Why it is built this way".
- `b11-config.md` (82 lines), `b11-reference.md` (routes A, B, C, common part, end), `b11-explainer.md` (What it is, How it works, Why it works this way, What has to happen), `b11-decision-tree.html`.

`b11` still needs a check and update for section 5 and 6 below (it predates the test suite), so it is not skipped.

## 4. State of each Phase B step

| Step | Build plan | Config | Reference | Explainer | Decision tree |
|---|---|---|---|---|---|
| b11 | Closed (67 lines) | Written | Written | Written | Written |
| b12 | Open: 216 lines of gathered sections | Old gathered material (25 lines) | Old (178 lines) | Empty (5 lines) | Old |
| b14 | Open: 222 lines | Old (25) | Old (262) | Empty | Old |
| b15 | Open: 1,200 lines, one "Carried over" block | Old (25) | Old (192) | Empty | Old |
| b16 | Open: 216 lines | Old (54) | Old (195) | Empty | Old |

"Gathered sections" are blocks headed `## From ...` (from old build notes, `pdlf-build-plan.md`, `pdlf-phase-b-review.md`, `pol-step-conditional-state.md`, `spec-execution-discipline.md`, `spec-artifact-handover.md`) and headings such as "Task list", "Learnings", "Open, not yet decided", "Global conventions applied throughout", "Later decisions", "Correction …". Closing the build plan means: each fact that is still true goes into the step entry or "Why"; everything else is removed; every "Open, not yet decided" item is decided (by Claude as engineer, asking David only about intent).

Specific to `b15`: its build plan holds a saved copy of the GStack `/plan-eng-review` skill (from line 262 on). That copy is from GStack 1.58.1. GStack is now pinned at 1.91.164 (`c580561`), where that skill changed. Remove the saved copy; check the step against the skill at `c580561` (public: `github.com/garrytan/gstack`, file `plan-eng-review/SKILL.md.tmpl` and `plan-eng-review/sections/`).

## 5. The test specs are the authority on testing

The test suite was built on 2026-10-21/22:
- `C:\dev\project-library-global\test-suite\`: `ts-method.md`, `ts-catalogue.md` (112 tests), `ts-conformance-checks.md`, `ts-rule-soundness-register.md` (empty), `tools\ts_scan.py`, `tools\ts_report.py`, `templates\` (`conftest.py`, `ts-config.yaml`, `access-matrix.yaml`, `pytest.ini`).
- Each step's `{step}-test-spec.md` names the catalogue tests the step runs ("Proves", a table of test IDs with "Applied here", "On failure").
- Security target: designed and reviewed against OWASP ASVS 5.0 Level 2 principles, with Level 3 controls on payment, administration and high-value transaction paths; evidence for SOC 2 Type II readiness, a yearly penetration test, PCI SAQ A, GDPR and POPIA.

Every build plan's **Testing** line becomes: "`{step}-test-spec.md`" plus one short sentence of what it proves. The config names the test spec; the reference includes running the tests and saving their evidence in `pdlf-outputs\{step}\`; the explainer says why.

Gaps found between the Phase B test specs and their build plans, to be closed in the build plans:

| Step | Test spec requires | Build plan today |
|---|---|---|
| b11 | PR-09 (local runtime, server and client Uplink keys, a `TEST_` user with a second factor, the mail catcher); ST-10 (each app's `.gitignore` covers `.env` and caches; `tests\` holds the four templates); PR-06 (no secret in any repository) | Testing is "the health check self-audit" only; the test setup (copy the templates into each app's `tests\`, `.env` keys `ANVIL_UPLINK_KEY`, `ANVIL_CLIENT_KEY`, `TS_TEST_PASSWORD`, start the App Server) is not in the step |
| b12 | DC-01 (every success criterion measurable); DC-02 (sections present; the 14 common aspects stated; no reference platform's technology carried over) | Testing names DC-01's idea only; DC-02 not named |
| b14 | DC-03 (scope; data inventory with protection levels; POPIA, GDPR, PCI SAQ A; exit; Hobby fit) | Not stated as outputs of the CEO plan |
| b15 | DC-04 (test plan with catalogue test IDs); DC-05 (`access-matrix.yaml`, complete and parsing); DC-06 (threat model over every trust boundary); DC-07 (security decisions: sign-in, sessions, secrets, logging, limits, outbound hosts, packages); DC-08 (common aspects met; conformance checks selected) | Produces "the reviewed plan and the test plan" and a threat model; `access-matrix.yaml`, the security decisions and the conformance selection are missing; Testing says "three levels" (the suite has levels D and 0 to 4) |
| b16 | DC-09 (one meaning per term; every entity owned and placed); PR-05 (receipts match evidence, via `ts_report.py --check`); PR-03 (gate approved) | PR-05 and the receipt check are not named |

## 6. Decisions and facts from this session the documents must reflect

Global rules corrected on 2026-10-22 (all in `project-library-global`, committed):
- Every client starts on the Anvil **Hobby** plan: background and scheduled tasks included; no persistent server; no staging; 1,000 emails a month, 150,000 rows, 10 GB.
- **Release:** App 1's tagged release is pushed into App 2 (`master_template`) by the developer at Step 42. No `develop`/`stable` branches. Testing before release is on the local Anvil App Server and a test client instance.
- **Testing location:** tests run first on the Anvil App Server on the developer's PC (empty database each run); only hosted services are tested on hosted App 1, with `TEST_` data. A server Uplink key sets up data only; a client Uplink key signed in as a role proves access.
- **Sign-in:** every account holder has a second factor (Anvil can require it only app-wide); the Owner uses FIDO2 only; shoppers buy as guests; remember-me at most 7 days; idle limit 30 minutes; passwords minimum 8, no composition rules, breached refused.
- **Server functions** return data and raise errors (no success/error envelope).
- **Money** in whole cents. **Observability:** instances push heartbeats; App 5 never polls.
- `spec-testing.md` moved out of the global library to `mb-3-cs-project-library\docs-local\mb-3-cs-test-specification.md`; `tmp-chklist-anvil-app-testing.md` deleted. Any step link to either must be redirected (to the test suite).
- `spec-vault-system.md` keeps the pattern; the `mb-3-cs` Vault contents moved to `mb-3-cs-project-library\docs-local\mb-3-cs-vault-implementation.md`.
- Ledger: `triage_findings.source_step` now also allows 35A, 38A, 40, 41, 42A, 43, 44 (live database and `spec-postgres-ledger.md`).
- New project files: `docs-local\schema-migration-log.md` (Step 17 records, Steps 41/42 read) and `docs-local\releases\v{n}\` for release specifications (Step 04).

Skills, pinned for PDLF (never upgraded without David's decision):

| Skill set | Version | Where OpenCode loads it |
|---|---|---|
| GStack | 1.91.164.0, commit `c580561`, branch `mybizz-c580561` (+ one local `.gitignore` commit) | `~/.config/opencode/skills/gstack-{name}/` (skill names unchanged, e.g. `cso`) |
| Matt Pocock | commit `5beb35b` | `~/.agents/skills/{name}/` |
| Anvil agent references | commit `14b1967` | `~/.agents/skills/{name}/` |
| Magdoub wireframe | `44a5814` | `~/.config/opencode/skills/wireframe/` |
| Magnus919 security skills | installed files | `~/.config/opencode/skills/` |

Also installed on 2026-10-22: the Anvil CLI 0.7.7 (signed in), the Anvil App Server 1.18.0 with Java 21, and the test tools (versions in `ts-method.md`). The skills catalog (`mybizz-os-docs\os-reference-docs\skills-catalog.md`) was updated to the installed state.

Step documents must name skills at these versions and check any skill behaviour they describe against these versions, not older notes.

## 7. How to work with David

- Read `preferences` in memory; they govern every reply.
- Before producing files: state the plan for the step (what changes in each of the five documents) and get approval. Then produce.
- One step at a time. Send that step's five files (plus any other file changed) in one batch.
- Send at most 16 files per send: the app shows only about 20, and larger sends lose files.
- With every send, list each file with the exact path it replaces.
- David saves the files and runs `bash /mnt/c/mybizz/scripts/commit-all.sh "message"`. The `mb-doc-check` hook converts `[[name]]` links to the standard form and blocks links to missing documents; write links as `[[name]]`.
- Work from the live repository (`git clone https://github.com/sassycomapp/pdlf`), never from an old copy: the hook rewrites links and dates on every commit, and a file built from a stale copy reverts those changes.
- WSL commands: one at a time; never in the same reply as an open question.
- Never edit `mybizz-config-docs` directly (it is written by `mb-config-manager` and `mb-sysdoc-creator`); never place files at `C:\` root.

## 8. Loose ends to close in the first batch

1. `pdlf-todo.md`: remove item E1 ("Verify Pass 1 against the installed copies"). It was resolved on 2026-10-22: Magdoub and Magnus919 matched; GStack, Matt Pocock and Anvil were brought to the pinned versions the steps were scoped from.
2. `app-factory-docs-update-method.md`: the two corrections in section 2.
3. OpenCode runs still pending on David's side (not part of this job): `/mb-sysdoc-creator anvil-cli`, `/mb-config-manager anvil-cli`, `/mb-config-manager gstack`.

## 9. First actions in the new session

1. Clone `sassycomapp/pdlf` and `sassycomapp/project-library-global` (current state).
2. Read `app-factory-docs-update-method.md`, `pdlf-build-plan.md` (Phase B section and build rules 4.x), the `b11` suite (the model), and `b11-test-spec.md`.
3. Present the plan for `b11` (its update for sections 5 and 6) and the two loose-end fixes; wait for approval.
4. Then `b12`, `b14`, `b15`, `b16`, one at a time, each with its plan first.
