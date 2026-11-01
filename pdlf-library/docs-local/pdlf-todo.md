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
2. `adr-no-free-trial.md`: no trial and no money-back guarantee; prospects use the demo apps (G6); every client instance runs on its own Mybizz-owned Anvil Business account.
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

## G. `mb-3-cs` features to carry into the design and architecture

### G0. Every G item reaches every document it touches

Each G item is written into every `mb-3-cs` document it affects, once the feature list is final, so PDLF Step 12 builds the build plan from documents that agree. The documents:

- `docs-local\`: `mb-3-cs-concept.md`, `mb-3-cs-architecture-explainer.md`, `mb-3-cs-architecture-reference.md`, `authoritative-schema.md`, `schema-migration-log.md`, `DESIGN.md`, `user-flows.md`, `custom-component-requirements-matrix.md`, `mb-3-cs-test-specification.md`, `mybizz-ai-implementation-spec.md`, `calendar-feature-spec.md`, `sm-syndication-spec.md`, `team-inbox-spec.md`, and `mb-3-cs-feature-list.md` (G1)
- `docs-standard-local\`: `business-requirements-document.md`, `product-requirements-document.md`, `software-requirements-specification.md`, `scaffold-spec.md`, `globals-contract.md`, `integration-architecture.md`, `observability-requirements.md`, `deployment-procedures.md`, `anvil-ui-build-standard.md`
- `policy-local\development-policy.md` and `adr-local\`, where a decision changes

The document lists in G2 to G11 name where each item lands first; G0 makes sure none is missed.

### G1. Feature list

The complete categorical feature list of `mb-3-cs` is saved as `docs-local\mb-3-cs-feature-list.md` and is the single source for features and marketing.

### G2. Front-end website editing

Owners and Managers see an Edit button on website pages, landing pages and published blog posts. Edit mode makes every text, image and video editable in place; Save publishes immediately, Cancel discards. In edit mode the AI helper writes or rewrites any selected text in the client's language; this is a new website-text assist in `mybizz-ai-implementation-spec.md`. New blog posts are created in BlogEditorForm and new landing pages in LandingPageEditorForm, where layout, SEO, tracking and scheduling are set.

### G3. App language

The client chooses the app's language: English, French, Portuguese, Spanish, German or Italian. English at launch; French, Portuguese and Spanish next; then German and Italian. From the first build, every screen text comes from a translation table (one row per phrase, one column per language) and is never typed into the Designer; every email template is stored per language; every help video is voiced or subtitled per language. AI (Groq) translates; a native speaker checks each language once. No right-to-left languages.

### G4. Team Inbox and email through Amazon SES

`docs-local\team-inbox-spec.md` specifies every email of `mb-3-cs`, received and sent, through Amazon SES: unlimited addresses on the client's domain in the Team Inbox, DKIM, SPF and DMARC written by App 5 into the client's Cloudflare DNS, campaigns with one-click unsubscribe and SES open and click tracking, suppression, and the 90-day archive to R2. Brevo is removed. Carry it into `authoritative-schema.md`, `integration-architecture.md`, `scaffold-spec.md`, `DESIGN.md`, `user-flows.md`, the concept (F-18, section 9.5), `mb-3-cs-architecture-reference.md` (F-18), `development-policy.md` (the approved exceptions: SES replaces Brevo) and the PRD. Before the first step that uses SES: confirm that `boto3` runs on Anvil's server Python, document SES with `mb-sysdoc-creator`, and confirm the SES receiving region.

David, once: open Mybizz's AWS account, request SES production access, and give Mybizz's Cloudflare user its name for clients to invite.

### G5. Sales features in the CRM

A deals pipeline (stages from lead to won or lost, with value and owner), companies (a business customer with several contacts) and quotes (accepted online, then converted to an invoice).

### G6. Demo apps

`demo.mybizz.live` holds sample data; `try.mybizz.live` starts empty. A scheduled task resets both every night. Every email is sent to the visitor's own address; payments run in each gateway's test mode with test cards.

### G7. Onboarding wizard and import

The wizard steps, in order: app language, business profile, brand palette, system currency, legal acknowledgement, payment gateway, connect the client's domain, import existing contacts. The import maps the columns of a CSV file, with ready-made mappings for HubSpot, Mailchimp and Acuity. Every step has a help video.

### G8. Help videos replace the setup call

Every feature has a short help video, opened from its tooltip in a pop-up, in the client's language. There is no guided setup call. Designed with E5.

### G9. Voice tiers 4 and 5 and sample data in the first build

Voice tiers 4 and 5 and the sample data are specified in `mybizz-ai-implementation-spec.md` and carried into the concept, the architecture reference and the PRD. Carry them into `authoritative-schema.md` (the `sample_rows` table), `scaffold-spec.md` (`sample_data_service` in `server_settings/`), `user-flows.md` (clearing the sample data), `mb-3-cs-test-specification.md` (tier 4, tier 5 and Clear sample data tests) and `DESIGN.md` (the sample data banner). David deletes `docs-local\releases\` once nothing links to it.

### G10. Social media syndication

`docs-local\sm-syndication-spec.md` specifies sharing each published blog post to Facebook, LinkedIn, WhatsApp and Instagram in one tap, with AI captions and full previews, using public share links only. Carry it into `authoritative-schema.md` (`blog_posts.share_captions`), `mybizz-ai-implementation-spec.md` (the social caption assist), `DESIGN.md` (the Share panel and reader share buttons), `user-flows.md` (UF-16), `scaffold-spec.md` (the blog post `Route.meta` tags and the `/_/api/blog-image/{slug}` endpoint) and `mb-3-cs-architecture-reference.md` (F-21).

### G11. The business model in the `mb-3-cs` documents

Carry the business model (E9) into the `mb-3-cs` documents: the concept (section 9 and F-33), F-04 (no upgrade feature: every client has its own account), the PRD capacity row (1,000,000 rows per client on its own Business account) and every other mention of a shared account, Brevo, the free trial or the money-back guarantee.

### G12. Built-in accounts replace the Wave integration

F-28 becomes Accounts, built into Mybizz CS: an expenses record (`expenses`: date, supplier, category, amount, tax, receipt image in R2, notes; `expense_categories`) beside the existing invoices, invoice items, payments and refunds; reports for profit and loss by month, outstanding invoices, tax collected and tax paid, and customer statements; one-click CSV export of customers, invoices, invoice lines, payments, refunds and expenses in the import formats of Wave, Xero and QuickBooks (dates `YYYY-MM-DD`, plain decimal amounts, no currency symbols, UTF-8, one file per record type). The Wave integration is removed. Carry it into the concept (F-28), `mb-3-cs-architecture-reference.md` (F-28), `mybizz-ai-implementation-spec.md` (Phase 5 and the Wave section removed), `authoritative-schema.md`, the PRD (US-27, FR-28), `integration-architecture.md`, `scaffold-spec.md` (`server_accounts/` replaces `server_integrations/wave_service`) and the sample data (three months of expenses).

### G13. R2 bucket layout

Each client's bucket uses these folders: `backups/daily/`, `backups/weekly/`, `history/{table}/`, `audit/{year}/{month}/`, `webhooks/{service}/{year}/{month}/`, `email/messages/{address}/{year}/{month}/`, `email/attachments/`, `expenses/receipts/`, `exports/`. Carry it into `integration-architecture.md` (Client Storage), `team-inbox-spec.md` and `mb-3-cs-architecture-reference.md` (F-29).
