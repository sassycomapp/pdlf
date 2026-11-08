---
title: "hosting-change-task-list"
doc-id: "mb-9e3a51d7"
updated: "2026-11-08"
---
# Hosting Change — Task List

Work list for bringing every live document into line with `mybizz-client-instance-hosting-proposal.md`. Each task names the file and the exact change. Batches run in order: each batch's files are delivered, saved and committed before the next batch starts.

---

## A. Supporting structures

| # | Structure | Location | Content |
|---|---|---|---|
| A1 | New specification `spec-client-instance-hosting.md` | `project-library-global/specifications-global/` | The canonical home of the proposal's sections 1 to 9: the five apps' hosting, the container, the image, the App Server settings, the container keys, the database and its sizes, releases, provisioning, client exit, uptime, costs. Every other document links to it instead of repeating it. |
| A2 | New code repository per business, `{slug}-app4` | `C:\dev\dev-{slug}\{slug}-app4`, GitHub `sassycomapp/{slug}-app4`, created in the App 3 run (Step 11, route C) | The client instance image: the image definition (`Dockerfile`), the container start script, the table-change check script, the image build workflow (GitHub Actions), and the pinned App Server version. Holds no application code. |
| A3 | Placeholder folder `(slug)-app4` | `project-template/dev-(SLUG)/` | Empty placeholder files with front matter for A2, so every business is created with it. |
| A4 | DigitalOcean platform set-up section | Inside `spec-client-activation-runbook.md` | One-time set-up per business: DigitalOcean project, Managed PostgreSQL cluster in `LON1`, registry repository, test client instance, API token in App 5's Vault. |
| A5 | Retire the proposal | `pdlf/pdlf-library/wip/mybizz-client-instance-hosting-proposal.md` | Deleted once batch 1 is committed. Its content lives in A1 and `adr-tiers-model.md`. |

---

## B. Batch 1 — `project-library-global` (17 files, about 2 hours)

| # | File | Change |
|---|---|---|
| 1.1 | `specifications-global/spec-client-instance-hosting.md` | New (A1). |
| 1.2 | `specifications-global/spec-five-app-architecture-model.md` | App 3: the client app every client container runs (startup module, full table definitions, `master_template` dependency). App 4: one container and one database per client on DigitalOcean. Update model: release image and App 5's Release action. Remove "Anvil cannot create tables programmatically". The rule "never add forms or server modules to a client instance" becomes "client-specific changes are made in App 1 only". |
| 1.3 | `adr-global/adr-client-instance-architecture.md` | Decision: client instance runs on the Anvil App Server on DigitalOcean. The App Server builds and extends the client's tables from App 3's definitions. The two proven Anvil behaviours stay. Schema consequence: additive changes apply on restart; removals are refused by the table-change check. |
| 1.4 | `adr-global/adr-dependency-update-model.md` | Update flow: App 1 tag → App 2 → release image → test client instance → App 5 Release action. Staged rollout and rollback by image tag. Account-failure consequences replaced by the DigitalOcean single-cluster consequence. |
| 1.5 | `adr-global/adr-dependency-based-not-multi-tenant.md` | App 3's role and App 4's hosting lines (lines 50 and 60). |
| 1.6 | `adr-global/adr-client-instance-readme-five-app-system.md` | Hosting lines 14, 18 and 19. |
| 1.7 | `adr-global/adr-tiers-model.md` | Price $99 a month per client; month to month, billed monthly in advance, cancel at any time effective at the end of the paid month; hosting line points to A1. |
| 1.8 | `adr-global/adr-mybizz-management-visibility.md` | Line 20: instances are App Server containers; line 104: `plan` is $99 a month. |
| 1.9 | `adr-global/adr-real-time-and-background-tasks.md` | Lines 79 and 95: background and scheduled tasks run inside each client's App Server container, with no timeout. |
| 1.10 | `adr-global/adr-no-free-trial.md` | Line 31: each paying client gets its own client instance from the first day. |
| 1.11 | `specifications-global/spec-deployment.md` | Sections 1, 2, 3, 4, 5, 7 and 8 rewritten to the image release, table-change check, rollback by image tag, DigitalOcean backups plus R2, and the DigitalOcean failure scenarios. |
| 1.12 | `specifications-global/spec-client-activation-runbook.md` | Provisioning steps from the proposal's section 6; A4 added; price $99 (lines 16, 94, 190). |
| 1.13 | `specifications-global/spec-nomenclature.md` | Lines 39, 65, 66 and 82: App 3 is the client app; App 4 has the repository `{slug}-app4` (the image) and runs on DigitalOcean. |
| 1.14 | `specifications-global/spec-anvil-platform-standards.md` | Line 55: plan section split into App 1, 2, 3, 5 (Anvil Business account) and App 4 (Anvil App Server, limits from A1). Line 328 kept. |
| 1.15 | `specifications-global/spec-mastertemplate-notification-system.md` | Line 84: tables come from App 3's definitions; line 240: background and scheduled tasks inside the App Server. |
| 1.16 | `specifications-global/spec-onboarding-implementation-plan.md` | Lines 426 and 435: $99 a month. |
| 1.17 | `policy-global/pol-common-aspects-for-mybizz-anvil-applications.md` | Aspect 2: each client instance has its own container and its own database; resources are raised per client. |
| 1.18 | `security-global/requirements/sec-requirements-pre-merge-master-template.md` | Line 10: a release reaches every client through App 5's Release action. |
| 1.19 | `test-suite/ts-conformance-checks.md` and `test-suite/ts-catalogue.md` | Architecture check and DC-02: "each client instance has its own container and its own database". |

---

## C. Batch 2 — `pdlf` (about 3 hours)

| # | File | Change |
|---|---|---|
| 2.1 | `app-factory/pdlf-build-plan.md` | Lines 63, 87, 95, 97 and 112: App 3 role, App 4 hosting, `{slug}-app4` repository, $99. |
| 2.2 | Step 7, all seven files (`a07-*`) | Step 7 creates App 3 and the `{slug}-app4` image repository (A2). |
| 2.3 | Step 8, all seven files (`a08-*`) | App 5's design inputs gain the DigitalOcean API actions: New client, Release, Remove, cluster capacity view. |
| 2.4 | Step 12, `b12-build-plan.md`, `b12-config.md`, `b12-explainer.md`, `b12-test-spec.md` | The Constraints line: each client instance has its own container and its own database. |
| 2.5 | Step 41, all files | Release readiness: the full test suite passes on the release image; the table-change check passes. |
| 2.6 | Step 42, all files | Release: App 2 updated, release image built and stored; client R2 backups before the release; rollback by image tag. Lines 27 to 30 rewritten. |
| 2.7 | Step 42A, all files | Regression test runs on the release image. |
| 2.8 | Step 43, all files | The test client instance moves to the new image and is smoke-tested. |
| 2.9 | Step 44, all files | Release: App 5's Release action, staged where the release is high-risk. |
| 2.10 | Step 45, all files | Production check reads every client's heartbeat for the release version. |
| 2.11 | Steps 41 to 46, line 11 of each build plan | "The release reaches every client instance through the release image." |
| 2.12 | `pdlf-library/pdlf-explainer-docs/pdlf-explainer.md` and `app-factory-explainer.md` | Line 153: hosting sentence. |
| 2.13 | `pdlf-library/adr-local/no-staging-environment-five-app-isolation.md` | Lines 22 and 23. |
| 2.14 | `pdlf-library/policy-local/pol-anvil-platform.md` | Line 49: client instances run App 3 and App 2 from the release image. |
| 2.15 | `pdlf-library/specifications-local/spec-postgres-ledger.md` | Line 79: client instances have no path; `{slug}-app4` sits beside the other app folders. The ledger's columns stay as they are. |
| 2.16 | `pdlf-library/wip/pdlf-session-handover.md` | Rewritten for the next session. |

---

## D. Batch 3 — `mybizz-os-docs` and `project-template` (about 30 minutes)

| # | File | Change |
|---|---|---|
| 3.1 | `mybizz-os-docs/os-reference-docs/repo-organization.md` | `{slug}-app4` rows for both businesses; line 70 naming note. |
| 3.2 | `project-template/dev-(SLUG)/README.md` | Line 15: App 4. |
| 3.3 | `project-template/dev-(SLUG)/(slug)-project-library/AGENTS.md` | Line 15: App 4. |
| 3.4 | `project-template/dev-(SLUG)/(slug)-app4/` | New placeholder folder (A3). |

---

## E. Batch 4 — `mb-3-cs-project-library` (about 3 hours)

| # | File | Change |
|---|---|---|
| 4.1 | `AGENTS.md` | Line 20: App 4. |
| 4.2 | `docs-local/mb-3-cs-architecture-reference.md` | Sections 2, 3, 4 and 5 to A1. |
| 4.3 | `docs-local/mb-3-cs-architecture-explainer.md` | Lines 42 and 53 onwards. |
| 4.4 | `docs-local/mb-3-cs-concept.md` | Price $99 (lines 220, 235, 519, 676); hosting lines 491, 529, 547; the money table (lines 556 and 557) recalculated from A1. |
| 4.5 | `docs-local/mb-3-cs-feature-list.md` | Lines 12 and 253. |
| 4.6 | `docs-local/user-flows.md` | Provisioning flow, lines 98 to 102. |
| 4.7 | `docs-local/strategy/pricing-strategy.md` | $99 and hosting basis. |
| 4.8 | `docs-local/design/app1/design-doc.md` | Lines 51, 62, 133, 437, 443 to 462, 669, 1055, 1122: hosting, capacity, money chain, AC-6 risk removed. |
| 4.9 | `docs-local/design/app1/threat-model.md` | Line 82: the Anvil hosting-terms risk is replaced by the DigitalOcean single-cluster risk. |
| 4.10 | `docs-standard-local/business-requirements-document.md` | BR-18, AC-5 to AC-8, the supplier row and risk row. |
| 4.11 | `docs-standard-local/product-requirements-document.md` | FR-33, capacity row, OQ-1 closed. |
| 4.12 | `docs-standard-local/software-requirements-specification.md` | Lines 35, 36, 73 and 187. |
| 4.13 | `docs-standard-local/deployment-procedures.md` | App 3 role, release and test client instance. |
| 4.14 | `docs-standard-local/client-exit-handover.md` | Line 46: container and database removed. |
| 4.15 | `docs-standard-local/integration-architecture.md` | Line 125: Python packages are installed in the release image; line 214 kept. |
| 4.16 | `adr-local/adr-blank-client-template.md` | App 3 as the client app in the release image; provisioning steps to A1. |

---

## F. Left unchanged

| File | Reason |
|---|---|
| Every `pdlf-outputs/` report | Records of completed PDLF runs. |
| `docs-local/design/app1/design-doc-first-concept.md` | Record of the first design concept. |
| Every "Data Tables view" line about App 1 | App 1 stays on Anvil Cloud, where those lines remain correct. |
| `docs-local/schema-migration-log.md` | Covers App 1 only. |
