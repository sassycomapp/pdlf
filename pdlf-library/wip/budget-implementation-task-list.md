---
title: "budget-implementation-task-list"
doc-id: "mb-a76874da"
updated: "2026-11-11"
---
# Budget Implementation — Task List

Work list for bringing every live document into line with section 7 of `Budget.md` (`C:\data-mybizz-mgt\business\Budget.md`). Each task names the file, the exact change and the Budget task numbers it carries out. Batches run in order: each batch's files are delivered, saved and committed before the next batch starts. Within a batch, no two files share a name; where a name repeats, the second file goes in the next round.

---

## A. Supporting structures — new files

| # | File | Location | Content | Budget tasks |
|---|---|---|---|---|
| A1 | `adr-fair-use-limits.md` | `project-library-global/adr-global/` | Every limit of Budget section 4: database connections, query time, idle transactions, database size, container memory, email volumes, email reputation, AI and voice spend, AI request rate, data transfer, client storage. How App 5 measures and enforces each limit, and the notice to the client and David at the warning and at the hard limit. The £1,700 Groq organisation spend limit. The acceptable-use terms and the `abuse@mybizz.live` address, with App 5's **Suspend** action. | 5, 10, 13 |
| A2 | `adr-automatic-resizing.md` | `project-library-global/adr-global/` | App 5 raises a client's container from 1 GiB to 2 GiB above 80% memory use, and the cluster from 8 GiB to 16 GiB at client 60. The largest size App 5 may choose, the notification to David, and the audit record. | 6 |
| A3 | `sec-cyber-essentials-compliance.md` | `project-library-global/security-global/compliance/` (new folder) | The whole-organisation scope; how each of the five controls is met; hardware security keys on every cloud service; AWS's root user kept unused; the asset and software register; the 14-day rule for high and critical fixes; the yearly renewal. Written against the NCSC requirements version 3.3 (Danzell question set). | 16, 21, 25 |
| A4 | `adr-business-insurance.md` | `project-library-global/adr-global/` | The combined policy (technology professional indemnity £1m, cyber liability £500,000, public liability £1m) and why each cover and limit; employers' liability before anyone other than David works for Mybizz; each policy condition with the safeguard that meets it and the test that checks it; yearly renewal. | 23 |
| A5 | `adr-company-compliance.md` | `project-library-global/adr-global/` | Mybizz-Live Ltd's statutory obligations: VAT registration from incorporation and the quarterly return, the confirmation statement, the annual accounts and company tax return from FreeAgent, the ICO fee, the UK address package; each deadline and its App 5 reminder. | 27 |
| A6 | `adr-freeagent-integration.md` | `project-library-global/adr-global/` | App 5's read-only connection to FreeAgent through its own FreeAgent user; what App 5 reads; credentials in App 5's Vault; the message to David when the connection fails. | 28 |
| A7 | `saas-tos-iro-paddle.md` | `mb-3-cs-project-library/legal-local/` and `project-template/dev-(SLUG)/(slug)-project-library/legal-local/` | The terms of service in respect of Paddle: Paddle as reseller and merchant of record, Paddle's invoices and receipts, refunds paid by Paddle on Mybizz's decision, price changes with advance notice, agreement to Paddle's buyer terms at checkout. | 36 |

---

## B. Batch 1 — `project-library-global` (about 3 hours)

Round 1: A1 to A6. Round 2: the updates below.

| # | File | Change | Budget tasks |
|---|---|---|---|
| 1.1 | `specifications-global/spec-client-instance-hosting.md` | Database section: Advanced Edition, standby from the first paying client, PostgreSQL 18, storage autoscaling, the capacity table (8 GiB: 197 connections, 65 clients; 16 GiB: 397 connections, 132 clients), TLS with full verification and `prepareThreshold=0` on every database address, trusted sources limited to DigitalOcean. Client database users with their three limits, created by the provisioning job inside DigitalOcean. Uptime section, pre-launch conditions with the reconnection test, Scenario B cost table, Sunday 06:00 UK maintenance window. Staged roll-out with health checks and automatic rollback, registry clean-up. Daily backup check and monthly restore drill. Heartbeat carries the database size. | 1, 2, 3, 8, 11, 17 |
| 1.2 | `specifications-global/spec-client-activation-runbook.md` | DigitalOcean platform set-up: Advanced cluster with standby, storage autoscaling, trusted sources, the provisioning job. Per client: database and user created with the settings of 1.1; client domain proxied through Cloudflare with the web application firewall, DDoS protection and bot blocking on; the nightly-copy bucket created with its 30-day retention lock. | 14, 17, 18, 19 |
| 1.3 | `specifications-global/spec-client-billing.md` | Cash-flow section on Scenario B: the £7.60 usage budget, the highest cost of one client (£52.98), every fixed cost of Budget section 1, VAT registration from incorporation, Paddle payouts without VAT, break-even at 9 clients. | 4, 25 |
| 1.4 | `adr-global/adr-mybizz-management-visibility.md` | App 5's functions: DigitalOcean connection with the two scoped keys; scheduled checks; both resize actions; fair-use enforcement; **Suspend** and **Rebuild**; audit record; daily summary and immediate messages; Cyber Essentials, insurance and statutory deadline reminders; FreeAgent tax timeline and Wise bank feed checks; the incident record. | 7, 22, 26 |
| 1.5 | `adr-global/adr-dependency-update-model.md` | Staged roll-out (test client instance, 10%, all) with health checks and automatic rollback; registry clean-up; images signed at build, run by digest, released only when the signature verifies; high and critical findings released within 14 days with messages on days 7 and 10; vendor-supported base image and Java runtime; a build containing end-of-life software fails. | 8, 20, 22 |
| 1.6 | `specifications-global/spec-deployment.md` | The **Rebuild** procedure: every client restored into a new Advanced cluster and new containers in another region, from DigitalOcean's backups or each client's nightly copy. The staged roll-out of 1.5. | 8, 15 |
| 1.7 | `specifications-global/spec-integration.md` | SES tenant reputation policy per client, the two CloudWatch alarms, the monthly email caps, 7-day deletion of received email files from S3. Cloudflare proxy on every client domain. FreeAgent read-only integration (A6). | 9, 19, 28 |
| 1.8 | `security-global/cloud/sec-email-service-trust-boundary.md` | The SES tenant reputation policy pauses one client's sending alone. | 9 |
| 1.9 | `adr-global/adr-observability-architecture.md` | App 5's status endpoint, the DigitalOcean Uptime check, the daily domain and certificate check, the data transfer and client storage checks. | 12 |
| 1.10 | `specifications-global/spec-observability.md` | The same checks as 1.9, with their thresholds and messages. | 12 |
| 1.11 | `security-global/infrastructure/sec-backup-recovery-integrity.md` | Daily backup check, monthly restore drill, 30-day retention lock on each nightly-copy bucket. | 11, 18 |
| 1.12 | `adr-global/adr-client-r2-storage-and-exit-handover.md` | The 30-day retention lock on each client's nightly-copy bucket. | 18 |
| 1.13 | `security-global/cloud/sec-client-provisioning-security.md` | The two DigitalOcean access keys and their custom scopes; the provisioning job inside DigitalOcean. | 13, 17 |
| 1.14 | `security-global/secrets/sec-secret-rotation-policy.md` | Yearly rotation of the two DigitalOcean keys, prompted by App 5 14 days before expiry. | 13 |
| 1.15 | `security-global/infrastructure/sec-database-access-control.md` | Trusted sources; per-client user limits; TLS with full verification. | 3, 17 |
| 1.16 | `specifications-global/spec-security-architecture.md` | Cross-references to A3, A4 and the incident response plans. | 16, 25 |
| 1.17 | `test-suite/ts-catalogue.md` | New tests: resize decisions and every fair-use limit against simulated suppliers; App Server reconnection after the database connection is cut; cluster is Advanced with a standby; each client database user carries its three limits; cluster refuses outside connections; a locked backup cannot be deleted; an unsigned image is refused; App 5 holds current insurance, Cyber Essentials and statutory dates and sends each reminder; FreeAgent connection against a sandbox company with no write made; the incident drill on the test client instance. | 40, 44 |
| 1.18 | `test-suite/ts-conformance-checks.md` | The conformance check for each new test in 1.17. | 40, 44 |

---

## C. Batch 2 — `mb-3-cs-project-library` (about 2.5 hours)

| # | File | Change | Budget tasks |
|---|---|---|---|
| 2.1 | `legal-local/saas-tos-iro-paddle.md` | New (A7). | 36 |
| 2.2 | `legal-local/client-service-agreement.md` | Fair-use limits and acceptable-use terms (A1); limitation of liability capped at the fees of the previous 12 months; breach notice to the client without undue delay; includes `saas-tos-iro-paddle.md`. | 32, 35, 36 |
| 2.3 | `docs-local/mb-3-cs-concept.md` | Section 9.6 Revenue model: Scenario B cost and profit figures, break-even at 9 clients. | 29 |
| 2.4 | `docs-local/mb-3-cs-architecture-reference.md` | App 5's automatic resizing, fair-use enforcement and notifications. | 30 |
| 2.5 | `docs-local/mb-3-cs-architecture-explainer.md` | The same, in explainer form. | 30 |
| 2.6 | `docs-local/DESIGN.md` | Section 8, Footer: the `abuse@mybizz.live` address on every public page. | 33 |
| 2.7 | `docs-standard-local/business-requirements-document.md` | Requirements for resizing, fair use, notifications, the incident record, the breach notice and the insurance renewal reminder. | 31, 37 |
| 2.8 | `docs-standard-local/product-requirements-document.md` | The same requirements at product level. | 31, 37 |
| 2.9 | `docs-standard-local/software-requirements-specification.md` | The same requirements at software level. | 31, 37 |
| 2.10 | `specifications-local/spec-test-specification.md` | One test per requirement of 2.7 to 2.9. | 31, 37 |
| 2.11 | `docs-standard-local/incident-response-plan.md` | Incident recorded in App 5; call to the insurer's incident line before any outside supplier; ICO report within 72 hours of a personal data breach; notice to affected clients without undue delay; evidence kept for the insurer. | 24 |
| 2.12 | `docs-standard-local/backup-and-recovery.md` | Daily backup check, monthly restore drill, 30-day retention lock. | 11, 18 |
| 2.13 | `docs-standard-local/observability-requirements.md` | The checks of 1.9. | 12 |
| 2.14 | `docs-standard-local/capacity-and-plan-tiers.md` | Container and cluster resize points. | 6 |
| 2.15 | `docs-standard-local/deployment-procedures.md` | Staged roll-out, signed images, the **Rebuild** procedure. | 8, 15, 20 |
| 2.16 | `docs-standard-local/integration-architecture.md` | SES tenant policy, email caps, Cloudflare proxy. | 9, 19 |
| 2.17 | `specifications-local/spec-ai-implementation.md` | Per-client metering of AI and voice spend, the £5.60 warning, the £16.80 stop, 20 requests a minute. | 10 |

---

## D. Batch 3 — `project-template` (about 1 hour)

Path prefix: `dev-(SLUG)/(slug)-project-library/`. Each file carries the business-independent content of its mb-3-cs counterpart in batch 2.

| # | File | Change | Budget tasks |
|---|---|---|---|
| 3.1 | `legal-local/saas-tos-iro-paddle.md` | New (A7). | 36 |
| 3.2 | `legal-local/client-service-agreement.md` | As 2.2. | 32, 35, 36 |
| 3.3 | `docs-standard-local/incident-response-plan.md` | As 2.11. | 24 |
| 3.4 | `docs-standard-local/backup-and-recovery.md` | As 2.12. | 11, 18 |
| 3.5 | `docs-standard-local/observability-requirements.md` | As 2.13. | 12 |
| 3.6 | `docs-standard-local/capacity-and-plan-tiers.md` | As 2.14. | 6 |
| 3.7 | `docs-standard-local/deployment-procedures.md` | As 2.15. | 8, 15, 20 |
| 3.8 | `docs-standard-local/integration-architecture.md` | As 2.16. | 9, 19 |

---

## E. Batch 4 — `pdlf` (about 1.5 hours)

| # | File | Change | Budget tasks |
|---|---|---|---|
| 4.1 | `app-factory/pdlf-build-plan.md` | Phase G "Must achieve": the DigitalOcean platform set-up of 1.2 with each item checked; the two DigitalOcean keys in App 5's Vault; the Uptime check on App 5's status endpoint; the two CloudWatch alarms; the Groq spend limit; the `{slug}-app4` workflows (weekly and per-build scan, image signing, report to App 5, registry clean-up, 14-day countdown, end-of-life check); the test client instance proxied through Cloudflare with its nightly-copy bucket locked. | 38, 39, 41, 42, 43 |
| 4.2 | Step 8, `a08-build-plan.md`, `a08-config.md`, `a08-explainer.md`, `a08-reference.md`, `a08-test-spec.md` | App 5's design inputs gain the functions of 1.4. | 7, 26 |
| 4.3 | Step 41, `f41-*` files | Release readiness: the image signature verifies; no high or critical finding older than 14 days; no end-of-life software. | 20, 22, 43 |

---

## F. Outside the batches

| # | Item | Where it goes |
|---|---|---|
| F1 | Budget task 34, the Cyber Essentials statement and badge, can only be added once the certificate is issued (before 1 April 2027). | `developers-duties.md`, once-off to-do, with this context. |
| F2 | Budget tasks 45 to 58 are David's. | Carried out in the order of `Budget.md` and `mybizz-live-business-setup.md`. |
