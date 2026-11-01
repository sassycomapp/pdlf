---
title: "pdlf-todo"
doc-id: "mb-13a3fbc9"
updated: "2026-11-01"
---
# Active PDLF To-Do List

Action items only. Completed and closed items are not tracked here.

---

## A. Building the steps

### A1. Rebuild Steps 17–46, one at a time

Steps 17–46 are audited and rebuilt one at a time as each phase is reached, with the same rigour as Steps 11/12/14/15/16. Each step is rebuilt with the build rules in section B and ends with `/mb-close-out`. Each rebuilt step writes the project's documents into the folders of the project template (`C:\dev\project-template\dev-(SLUG)\`), as each folder's `README.md` names them. Each phase is built, proven on `mb-3-cs` and finished in the order the [[[pdlf:pdlf-library/docs-local/app-factory-docs-update-method|App Factory Docs Update Method]]](C:/pdlf/pdlf-library/docs-local/app-factory-docs-update-method.md) sets out.

### A2. Prove Phases A and B on `mb-3-cs`

Phases A and B are built. They are proven by running `mb-3-cs` through them by entry point 03, in this order:

1. David installs the `pdlf-init` skill with the command in [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md).
2. Cupcake's rule `no_agent_gate_approval` is compiled with `/mb-compile-rules` and tested by David, block case and allow case.
3. David proves with `cupcake eval` that, with OpenCode opened in `projects/mb-3-cs-app1`, a write to `/mnt/c/dev/dev-mb-3-cs/mb-3-cs-project-library` is allowed and a write to `/mnt/c/pdlf` is blocked.
4. David runs `bash /mnt/c/mybizz/scripts/pdlf-gate.sh --check`, which must print `ledger answers`.
5. David backs up `C:\dev\dev-mb-3-cs\`.
6. David opens `projects/mb-3-cs-app1` in OpenCode, runs `/pdlf-init` and takes entry point 03. The project context `mb-3-cs-project-context` is already moved, so Step 11 checks it and makes the new `mb-3-cs-project-library` from the template.

Whatever fails or is missing is corrected in PDLF, and the run continues from the step corrected.

---

## B. Rules for building every step

### B1. Global-content query-fetch-apply sequence

The rule and its enforcement are set by [[[pdlf:pdlf-library/adr-local/global-content-discovery-and-application-discipline]]](C:/pdlf/pdlf-library/adr-local/global-content-discovery-and-application-discipline.md) and [[[pdlf:pdlf-library/policy-local/pol-memory-and-knowledge]]](C:/pdlf/pdlf-library/policy-local/pol-memory-and-knowledge.md). Every documentation repository is a federated GBrain source, so one search covers everything, and cross-repository links use the standard form `[[[source-id:slug]]](C:/full/path.md)`, written by agents as `[[name]]` and converted by the `mb-doc-check` commit hook. The five-step sequence and its citation requirement are built into each relevant step file (17, 20, 22, 26, 27, 35, 35A, 37, 38, 41–45 at minimum) as that step is rebuilt under A1, after the sequence is checked against that setup.

### B4. End-to-end proof of the governed memory pipeline

The governed memory pipeline is proven end to end, once, on the first real step run on `mb-3-cs`.

---

## C. Testing

### C3. Secret scan at every commit

`commit-all.sh` runs `gitleaks` on each repository before it commits, and stops that repository's commit when a secret is found, so a key can never reach a public repository again. Built once Phase B is proven.

### C2. Prove the test suite on `mb-3-cs`

When `mb-3-cs` first runs through Phase B, Step 11 runs PR-09 to prove the local runtime, both Uplink connections, the `TEST_` users with second factors and the mail catcher; each later step then runs its test specification. The local runtime is started with `ts_local.sh`; an app that uses dependency apps (the Material 3 theme, routing) also needs them served to the App Server, which is settled on this first run. Correct any test, template or tool that does not work as written before another application relies on it.

---

## E. Skills and documentation

### E1. Verify the security skills and GBrain results against the steps

For each phase, before it is proven: compare the two Magnus919 security skill files installed in `~/.config/opencode/skills/`, and the GBrain results the steps were scoped from, with the steps that use them. Correct any step that does not match.

### E2. Anvil's `$app-testing` skill

Anvil's `data-models` and `server-code` skills call `$app-testing`, and `anvil-yaml` calls `anvil db apply-schema --force`, to test against the agent's temporary database. `$app-testing` is not yet published in `anvil-agent-references`. When Anvil publishes it, it is assessed as a complement to the local runtime of the test suite, and examined whenever `anvil-agent-references` is updated.

### E5. Help and video documentation

Design the user help documentation and the video documentation, as one design job, before Phase E is built.

### E8. Cloudflare R2

Each client has one R2 bucket in a free Cloudflare account in the client's own name, on the client's own email address; Mybizz is an invited member with the role Cloudflare R2 Admin, and App 5 creates the bucket and its token (`mb-3-cs` `integration-architecture.md`, Client Storage). Cloudflare is registered Deferred in the skills catalog; document it with `mb-sysdoc-creator` before the first step that uses it, and confirm which S3-compatible library runs on Anvil's server Python.

### E9. Global ADRs to bring in line with the Mybizz business model

The same business model applies to every Mybizz business: $150 a month per client, month to month with no contract; each client instance on its own Mybizz-owned Anvil Business account; unlimited staff logins; no add-ons; no free trial and no money-back guarantee, replaced by two demo apps. The global ADRs in `C:\dev\project-library-global\adr-global` that state it wrongly are corrected before the next PDLF run reads them at Step 12:

1. `adr-tiers-model.md`: one price, $150 a month per client; assisted setup at $200 once.
2. `adr-no-free-trial.md`: no trial and no money-back guarantee; prospects use the demo apps (`mb-3-cs` F-36); every client instance runs on its own Mybizz-owned Anvil Business account.
3. `adr-client-r2-storage-and-exit-handover.md`: one bucket in a free Cloudflare account in the client's own name; Mybizz is an invited member; at exit the export is written into the bucket and Mybizz leaves the account.
4. `adr-dependency-based-not-multi-tenant.md`, `adr-dependency-update-model.md`, `adr-client-instance-readme-five-app-system.md`, `adr-real-time-and-background-tasks.md` and `adr-mybizz-management-visibility.md`: each client instance is on its own Mybizz-owned Anvil Business account, not the client's own account, and App 5 is built before launch.

The same correction applies to `spec-deployment.md`, the PDLF Step 12 file (`b12-build-plan.md`) and `pdlf-build-plan.md`, which state that every client starts on the Hobby plan.

---

## F. Applications

### F1. Make `mb-4-ecom` in a copy of the project template

`mb-4-ecom` enters PDLF by entry point 03 after `mb-3-cs`. Step 11 makes it in a copy of the project template, as for `mb-3-cs` (A2), with its existing repositories as the context it brings, and moves its Medusa material from the project library's `wip\` into `reference-platform-local\` (`source\`, `reference\`, `notes\`) with David's permission. Until then, nothing in `mb-4-ecom` is moved. Before its run, each of its app folders' `opencode.json` allows the Build agent's shell commands (`bash` `"*": "allow"`, with the Plan agent's `bash` `"*": "ask"`), as in `mb-3-cs-app1`, so OpenCode does not ask before every command.

### F2. Make the project template general after each business

When a business is finished, every item its design marked `common` that is not yet in the project template is made general and placed there ([[[default:adr-global/adr-common-and-trade-modules]]](C:/dev/project-library-global/adr-global/adr-common-and-trade-modules.md)), so the next business starts from it. Done first when `mb-3-cs` is finished.

---

## G. `mb-3-cs` before its PDLF run

The `mb-3-cs` project context (`docs-local\`, `docs-standard-local\`, `policy-local\`, `adr-local\`) holds the complete, consistent design of every feature in `mb-3-cs-feature-list.md`.

### G1. Before the first step that uses SES

Confirm that `boto3` runs on Anvil's server Python, document Amazon SES with `mb-sysdoc-creator`, and confirm that SES receives email in `eu-west-1`.

### G2. Personal data sent through App 5

The PRD (Data protection) states that no customer personal data is sent to App 5. Voice tiers 1 to 4 send speech, which can name customers, through App 5 to Groq for transcription; AI assists 6 and 9 send email and communication text. Decide the rule for AI and voice requests through App 5 (pass through without storing, or names removed before sending) and write it into the PRD, the SRS and `mybizz-ai-implementation-spec.md`.

### G3. David, once

1. Open Mybizz's AWS account and request SES production access.
2. Set up Mybizz's Cloudflare user, which clients invite with the roles Cloudflare R2 Admin and DNS.
3. Delete `docs-local\releases\` and `docs-local\Anvil Email System — Developer Brief.md`.
4. Ask Anvil's sales team in writing whether Mybizz may run each client's business app on a Mybizz-owned Business account (BRD AC-6).
