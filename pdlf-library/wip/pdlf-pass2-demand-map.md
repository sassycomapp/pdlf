---
title: "pdlf-pass2-demand-map"
updated: "2026-10-29"
doc-id: "mb-91e25269"
---
# PDLF Pass 2 — Demand Map

Working file for Pass 2 of the skills scoping strategy. It lists what `mb-3-cs` and `mb-4-ecom` demand of PDLF, where each demand comes from, which steps it touches and what it means for those steps' skills. Pass 2 walks every step against this map and corrects the step build plans. When Pass 2 is complete, this file is deleted.

## Sources read

- `mb-3-cs-project-context`: `adr-local` (3), `docs-local` (20), `policy-local/development-policy.md`, `V2/mybizz-ai-implementation-spec-v2.md`, `V3/mybizz-ai-implementation-spec-v3 (1).md`.
- `mb-4-ecom-project-library`: `docs/report from discussion with gemini.md`.
- `project-library-global`: the decision of every ADR in `adr-global` (44); `spec-integration`, `spec-security-architecture`, `spec-vault-system`, `spec-regulatory-compliance-baseline`, `spec-deployment`, `spec-mastertemplate-notification-system`, `spec-api-specification`, `spec-client-activation-runbook`.

## The two applications

- **`mb-3-cs`** (Mybizz Consulting & Services): a complete online business for service businesses: public website, service catalogue, bookings and calendar, payments and invoicing, CRM, three email systems, campaigns, landing pages, blog, tasks, dashboard and analytics, settings and the Vault. 44 tables. V1 is largely designed and partly scaffolded; V2 (AI assists and voice) and V3 (voice intelligence, Wave Accounting) are planned feature releases.
- **`mb-4-ecom`** (Mybizz e-commerce): the same five-app architecture and infrastructure as `mb-3-cs`, oriented to e-commerce, with Medusa.js as the reference design for its schema, workflows and order state machines, rewritten in Python for Anvil. Not yet designed.
- **Shared:** the five-app structure, one isolated app and database per client, Material 3, the Vault, payments, webhooks, Brevo email, Mybizz_management (App 5) and Cloudflare R2 for offloaded storage.

## Demands

Each demand: what it is · source · steps it touches · what it means for skills.

### D1. Existing context enters through Step 03

- `mb-3-cs` arrives with 20 design documents, 3 local ADRs, a 44-table schema and a scaffolded App 1, written before PDLF.
- Source: `docs-local/INDEX.md`, App 1.
- Steps: a03, b11 (route B), b12, b16.
- Skills: `graphify` on App 1 at b11; b12 must separate the concept from the existing documents, which include strategy, pricing and positioning documents, not only a design; b16 must reconcile the existing `CONTEXT.md` (incomplete) with `authoritative-schema.md`.

### D2. Features arrive as versioned releases (V1, V2, V3)

- V2 and V3 are each a wave of features built after V1 is live.
- Source: V2 and V3 specifications.
- Steps: a04, a05, b12 (feature path), c19, f41–f46.
- Skills: the feature path must accept a whole release specification (many features) and break it into tickets with `to-tickets`; Steps 41–46 run per release.

### D3. Schema changes must reach App 3 and every client instance

- A schema change must be applied to `blank_client_template` and to every existing client instance by hand; no schema change is released without a documented migration plan; schema cannot be rolled back automatically.
- Source: `adr-local/blank-client-template.md`, `spec-deployment` sections 4 and 5.
- Steps: c17, f41, f42, f43, f44, Phase G.
- Skills: the release steps lack a schema-migration task; `wizard` fits the per-instance manual migration; `anvil-yaml` writes the schema; a pre-migration backup is required.

### D4. Staged rollout and rollback

- High-risk releases are rolled out with version tags to a subset of client instances first; rollback is re-pointing to the last good commit and republishing, not a revert.
- Source: `spec-deployment` sections 3 and 4.
- Steps: f42, f43, f44, f45.
- Skills: Step 42's rollback text must follow the specification; `/canary` per rolled-out instance at f43 and f45.

### D5. Payments: Stripe and Paystack, one gateway per instance

- Payment processing, webhooks (immediate 200, then a background task), idempotency, failure recovery (15-minute hold), PCI DSS where it applies.
- Source: `spec-integration`, `spec-api-specification`, `adr-webhook-architecture`, `adr-payment-gateway-*`, `user-flows` section 6.
- Steps: b15, c19, e35, e35a, e37, e38.
- Skills: `secure-software-engineering` and `/cso` on payment and webhook code; webhook handlers need integration tests against the gateways' test modes, which the testing layer does not yet name (Pass 3).

### D6. Email: three systems (Anvil, Brevo SMTP, Brevo Campaigns) and Brevo webhooks

- Source: `adr-brevo-replaces-zoho-email`, `spec-integration`.
- Steps: b15, e35, e38.
- Skills: as D5 for webhooks; email content testing belongs to Pass 3.

### D7. The Vault and secrets

- An application-level encrypted secrets store, Owner-only, with TOTP recovery; one Anvil Secret (`encryption_key`).
- Source: `spec-vault-system`, `development-policy` section 1.
- Steps: b14, b15, c17, d34, e35, e37.
- Skills: Sentinel at Very High on any Vault code; `security-audit-methodology` at d34 and f41.

### D8. Background tasks and polling

- Hourly campaign processing, nightly metrics at 2 a.m., reminders 24 hours and 1 hour before bookings; near-real-time updates by client-side polling.
- Source: `adr-real-time-and-background-tasks`, `user-flows` sections 8 and 9.
- Steps: b15, e35, e38.
- Skills: `server-code` (background tasks); scheduled behaviour needs time-controlled tests (Pass 3).

### D9. PDF invoices

- Server-side PDF generation on booking completion, sent by email.
- Source: `adr-pdf-invoice-generation`.
- Steps: b15, e35.
- Skills: `server-code`; the PDF library must run on Anvil's server Python (checked at b15 platform fit).

### D10. Public website with routing, landing pages and blog

- Public pages use the Anvil routing dependency; admin uses Links and `open_form`; four homepage templates; three landing-page templates; SEO settings on posts.
- Source: `architecture.md`, `user-flows` sections 4, 10, 11, 13.
- Steps: c20, c22, c26, c27, d29, e36, e38.
- Skills: `client-forms`; `/qa-only` must cover public pages unauthenticated; `benchmark` (GStack) fits public page performance and is not yet used.

### D11. Strict Material 3, banned components and custom components

- Only M3 dependency components; Anvil Extras and `HTMLTemplate` banned; five shared custom components (video, footer, carousel, parallax, ClauseBuilder); dark mode in V1; card radius 8 px.
- Source: `adr-material-3-theme-component-scope`, `adr-anvil-extras-exclusion`, `adr-htmltemplate-use`, `adr-dark-mode-v1`, `custom-component-requirements-matrix.md`, `design-direction.md`.
- Conflict: `calendar-feature-spec.md` uses `HTMLTemplate` for the month grid, which `adr-htmltemplate-use` bans.
- Steps: c20, c22, c26, c27, d29, d31, e35, e36.
- Skills: `client-forms` (custom component forms); custom components need their own design and test path, which the steps do not name.

### D12. Onboarding, legal acknowledgement and policies

- Resumable onboarding; currency immutable after the first transaction; Owner acknowledges legal responsibility; ClauseBuilder writes the Privacy Policy and Terms; POPIA mandatory, GDPR and PCI DSS conditional; data export and offboarding.
- Source: onboarding ADRs, `adr-legal-policy-…`, `adr-client-data-management-rights-…`, `spec-regulatory-compliance-baseline`.
- Steps: b14, b15, c19, e35, f41.
- Skills: regulatory baseline at b14 (already named); a compliance check before release at f41 is not yet named.

### D13. App 5 and the management endpoints

- Client instances expose management HTTP endpoints from day one, secured with per-client Bearer tokens; App 5 collects observability metrics; heartbeat pushed from App 4 to App 5.
- Source: `adr-mybizz-management-visibility`, `adr-observability-architecture`, `spec-api-specification`, Gemini report section 3.
- Steps: a08, b15, e35, Phase G.
- Skills: `secure-software-engineering` on token handling; App 5 is built through a08 and Phase G.

### D14. Provisioning a client instance (App 4)

- Clone App 3, set Secrets, domain, management token, registry, Owner, Vault, webhook registration.
- Source: `spec-client-activation-runbook`, `adr-client-instance-readme-five-app-system`.
- Steps: Phase G.
- Skills: `wizard` fits the runbook; the client-instance README is a deliverable.

### D15. AI and voice (V2, V3)

- One reusable AI helper component; Groq Whisper for speech-to-text (server-side); browser speech synthesis; a shared AI request pipeline; prompts kept modular; AI is an enhancement, never a dependency.
- Source: V2 and V3 specifications.
- Steps: b15, c19, e35, e37, e38.
- Skills: external AI providers' keys go in the Vault; no installed skill covers prompt design or evaluation of AI output; testing AI features belongs to Pass 3.

### D16. Wave Accounting (V3)

- Connected once in Settings; credentials in the Vault.
- Source: V3 specification.
- Steps: as D5 (integration).

### D17. Cloudflare R2 offloading (shared with `mb-4-ecom`)

- Raw webhook payloads, logs and backups offloaded to R2 under per-client keys.
- Source: Gemini report section 5; Cloudflare is registered Deferred in the skills catalog's systems.
- Steps: b15, e35, Phase G.
- Skills: no installed skill covers Cloudflare; R2 credentials go in the Vault.

### D18. E-commerce specifics (`mb-4-ecom`)

- Medusa.js as reference design (Python re-implementation), metadata fields for client-level customisation, B2B features, multi-channel inventory sync, idempotent order handling.
- Source: Gemini report.
- Steps: b12 (reference design), b15, b16, c17.
- Skills: `research` (Matt Pocock) fits reading the Medusa reference against primary sources; the Medusa and REA source archives sit in `mb-4-ecom-project-library/docs/`.
- Conflict: the report calls the structure "multi-tenant", which `adr-dependency-based-not-multi-tenant` forbids as a term and a pattern; the structure it describes is the isolated five-app model.

### D19. Mybizz-specific content in the global library

- `project-library-global` holds decisions and specifications that are specific to `mb-3-cs` (tiers, onboarding, payment gateways, ClauseBuilder, the "Mybizz CS" screen and UI standards, the Vault build sequence for `mb-3-cs`).
- Steps: b14, b15 (the comparison with `project-library-global`).
- Action: sort them: what applies to every Mybizz business stays global; what applies only to `mb-3-cs` moves to its project library. `mb-4-ecom` shares most of them, so many stay global.

### D20. Stale documents in the `mb-3-cs` library

- `CONTEXT.md` names the wrong folders (`C:\projects\`), the old repository name and the old to-do list; `gstack-artifact-governance.md` names folders that no longer exist; `development-policy.md` names VS Code with Continue.dev and a `master`/`dev` branching model; `architecture.md` names the `develop` → `stable` release.
- Steps: a03, b12, b16.
- Action: b12 and b16 treat these as prior material to be checked, not as fact.
