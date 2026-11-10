---
title: "pdlf-todo"
doc-id: "mb-13a3fbc9"
updated: "2026-11-10"
---
# Active PDLF To-Do List

Action items only. Completed and closed items are not tracked here.

---

## A. Building the steps

### A1. Rebuild Steps 17–46, one at a time

Steps 17–46 are audited and rebuilt one at a time as each phase is reached, with the same rigour as Steps 11/12/14/15/16. Each step is rebuilt with the build rules in section B and ends with `/mb-close-out`. Each rebuilt step writes the project's documents into the folders of the project template (`C:\dev\project-template\dev-(SLUG)\`), as each folder's `README.md` names them. Each phase is built, proven on `mb-3-cs` and finished in the order the [[[pdlf:pdlf-library/docs-local/app-factory-docs-update-method|App Factory Docs Update Method]]](C:/pdlf/pdlf-library/docs-local/app-factory-docs-update-method.md) sets out.

### A1a. Phase C UI tools before Step 17

Phase C (Steps 17–28) is rebuilt to the [[[pdlf:pdlf-library/wip/pdlf-phase-c-ui-workflow|PDLF Phase C — UI Workflow]]](C:/pdlf/pdlf-library/wip/pdlf-phase-c-ui-workflow.md). Its batch 5 is done before Step 17 is rebuilt: the test suite scanner reads HTML forms and checks them against `m3-custom-theme`; `ts-config.yaml`, `spec-component-properties.md` and `spec-nomenclature.md` are rebuilt from the theme's documentation; `mb-form-builder` is written, installed and documented, and checks after each run that no form of the feature still has a `form_template.yaml`; `skills-catalog.md` registers it; Steps C17 to C28 are rebuilt to [[[default:specifications-global/mo-ui-production|UI Production]]](C:/dev/project-library-global/specifications-global/mo-ui-production.md).

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

### B1. Canonical folders in every rebuilt step

The canonical-sources rules are set by [[[pdlf:pdlf-library/policy-local/pol-memory-and-knowledge]]](C:/pdlf/pdlf-library/policy-local/pol-memory-and-knowledge.md) (Canonical sources) and [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) (substep 1). Steps 12, 14, 15 and 16 carry their Canonical folders table. Each of Steps 17–46 gets its own table as it is rebuilt under A1.

### B2. Skills fit in every rebuilt step

The skills catalogue (`C:\mybizz\mybizz-os-docs\os-reference-docs\skills-catalog.md`) is a starting point, not a limit. As each step is rebuilt under A1, Claude checks every need of the step against the catalogue. For each need no catalogued skill covers well, Claude searches outside it: Anvil's agent references first, then trusted skill collections on GitHub, then the wider web. Each skill found is checked against [[[pdlf:pdlf-library/adr-local/skill-use-principle]]](C:/pdlf/pdlf-library/adr-local/skill-use-principle.md): it works on Anvil, it is maintained, and its source is trusted. David approves or rejects it; an approved skill is added to the catalogue with its PDLF steps. During a run, an agent that meets a need no skill covers raises a flag, and the gap is closed in PDLF.

The `mb-3-cs` design's needs, checked:

| Need | Skill | Status |
|---|---|---|
| Amazon SES: sending, tenants, identities, events | `aws-ses` (AWS, `amazon-ses/skills`) | To install |
| Cloudflare: R2 storage and DNS records | `cloudflare` and `cf-cli` (Cloudflare, `cloudflare/skills`) | To install |
| PayPal checkout, orders, refunds, webhooks | `paypal-best-practices` and `paypal-routing` (PayPal, `paypal/AI-Toolkit`) | To install |
| The app in six languages | A MyBizz skill written by Claude from `spec-translation.md` | To write, then install |
| Amazon SES receiving | SES's receiving documentation | No skill needed |
| Accounting export formats | Each vendor's import template, read at Step 15 | No skill needed |
| Voice and AI through Groq | Groq's API documentation | No skill needed |
| Help videos | David's video tools; designed at E5 | No skill needed |

The skills marked "To install" are installed together once David settles the install list.

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

---

## F. Applications

### F1. Make `mb-4-ecom` in a copy of the project template

`mb-4-ecom` enters PDLF by entry point 03 after `mb-3-cs`. Step 11 makes it in a copy of the project template, as for `mb-3-cs` (A2), with its existing repositories as the context it brings, and moves its Medusa material from the project library's `wip\` into `reference-platform-local\` (`source\`, `reference\`, `notes\`) with David's permission. Until then, nothing in `mb-4-ecom` is moved. Before its run, each of its app folders' `opencode.json` allows the Build agent's shell commands (`bash` `"*": "allow"`, with the Plan agent's `bash` `"*": "ask"`), as in `mb-3-cs-app1`, so OpenCode does not ask before every command.

### F2. Make the project template general after each business

When a business is finished, every item its design marked `common` that is not yet in the project template is made general and placed there ([[[default:adr-global/adr-common-and-trade-modules]]](C:/dev/project-library-global/adr-global/adr-common-and-trade-modules.md)), so the next business starts from it. Done first when `mb-3-cs` is finished.

---

## G. `mb-3-cs` before its PDLF run

The `mb-3-cs` project context (`docs-local\`, `docs-standard-local\`, `policy-local\`, `adr-local\`) holds the complete, consistent design of every feature in `mb-3-cs-feature-list.md`.

### G1. Before the first step that uses SES or R2

Document Amazon SES and Cloudflare with `mb-sysdoc-creator` (both are registered Deferred in the skills catalog).

### G2. Align the design to the M3 custom theme's palettes

The M3 custom theme (`m3-custom-theme`, version `v2.0.0`) holds eight palettes, each light and dark: `default`, `professional_blue`, `warm_coral`, `calm_teal`, `sophisticated_purple`, `sky_blue`, `forest_green` and `desert_rose`. The theme's module `m3x_theming` applies a palette and the light or dark mode (`set_palette`, `set_mode`, `apply_saved`). How the theme's colours work is in `m3-custom-theme.md`, Section 4, in `m3-custom-theme-project-library`.

The `mb-3-cs` design still describes four palettes, its own palette module (`shared/palette_utils.py`) and its own colour values in `palette-tokens.md`. The design is aligned as follows:

1. Delete `docs-local/palette-tokens.md`; the theme holds the colours.
2. Remove the module `shared/palette_utils.py` from the design; at start-up, App 1 calls `m3x_theming.set_palette` with `business_profile.palette`.
3. List the eight palette names, default `professional_blue`, and remove every reference to `palette-tokens.md` and `palette_utils.py`, in: `docs-standard-local/authoritative-schema.md`, `globals-contract.md`, `custom-component-requirements-matrix.md`, `software-requirements-specification.md`, `scaffold-spec.md`, `product-requirements-document.md`, `business-requirements-document.md`; `docs-local/mb-3-cs-architecture-reference.md`, `mb-3-cs-architecture-explainer.md`, `DESIGN.md`, `design/app1/design-doc.md`.

Every other Anvil app that added the theme before 10 November 2026 holds an old copy of the theme's colour list in its own `theme/parameters.yaml`. Apps 2, 3 and 5 and `mb-4-ecom` are checked; each one that has the theme gets the theme's `theme/parameters.yaml`, the same fix as App 1.

### G3. David, once

1. Open Mybizz's AWS account and request SES production access.
2. Set up Mybizz's Cloudflare user, which clients invite with the roles Cloudflare R2 Admin and DNS.
3. Switch on Zero Data Retention in the Groq console (Settings → Data Controls) for Mybizz's Groq organisation (SR-53a).
4. In the Anvil editor, switch App 1 to Python 3.14 (Settings → Python versions); App 2 already runs it.
5. In the Anvil editor, App 1's Users service: "Require 2-factor authentication" on, with "Allow 2-factor reset by email" on.
6. Open Mybizz's Paddle account and complete Paddle's approval of the business; create the subscription product with its fixed monthly prices before tax, £79, $99, C$135, €89 and CHF 89, and limit the checkout to Mybizz's markets ([[[default:specifications-global/spec-client-billing|Client Billing]]](C:/dev/project-library-global/specifications-global/spec-client-billing.md)).
7. In Mybizz's Cloudflare account, create Mybizz's own R2 bucket for App 5, which holds Paddle's billing notifications.
8. Register Mybizz-Live Ltd for UK VAT at incorporation, as an intending trader; the accountant confirms how Paddle's reverse invoices are entered on the VAT return.
9. Register Mybizz-Live Ltd with the Information Commissioner's Office and pay its data protection fee, before launch.

### G4. Export layouts for Wave, Xero and QuickBooks

The Accounts screen of App 1 has three buttons: "Download for Wave", "Download for Xero" and "Download for QuickBooks", with one period (From and To dates, last month by default). Each button downloads one ZIP file holding the period's full books: customers; invoices with their lines and tax; payments and refunds; expenses. Each file is laid out in the exact import format of that package. The column layout of every file for each of the three packages is specified in `docs-standard-local/integration-architecture.md`, and feature-list section 23, FR-28 and SR-48 are brought into line with it.

### G5. Remove Paystack and Portuguese from App 1

The design keeps Stripe as the only card gateway, with PayPal optional, and five languages: English, French, German, Spanish and Italian. App 1's code and tables are brought into line:

1. Remove `server_payments/paystack_service.py` (or `paystack_gateway`), and every call to it.
2. Remove the `paystack_public_key`, `paystack_connected`, `paystack_connected_at` and `active_gateway` columns from `payment_config`, and `paystack` from every `method` and `gateway` value list.
3. Remove the Paystack option from Settings → Payment Gateways and from the onboarding wizard.
4. Remove the Portuguese phrase file (`shared/translations/pt.py`) and `pt` from the language list.
