---
title: "mybizz-client-instance-hosting-proposal"
doc-id: "mb-4c8257ec"
updated: "2026-11-08"
---
# Mybizz — Client Instance Hosting Proposal

**Scope:** Mybizz-wide. Covers where and how every client instance (App 4) runs, what it costs, and the commercial terms Mybizz offers clients. Applies to every Mybizz business.

---

## 1. The Solution

- Every client instance runs on DigitalOcean's fully managed services, using the free, open-source Anvil App Server.
- Apps 1, 2, 3 and 5 stay on Mybizz's one Anvil Business account.
- Each client instance is one container on DigitalOcean App Platform, with its own database in one DigitalOcean Managed PostgreSQL cluster.
- DigitalOcean runs the servers, security updates, failover and database backups. Mybizz runs no server.
- Mybizz sells each client instance at $99 a month, month to month, with no contract.

---

## 2. The Five Apps

| App                             | Runs on                                          | Role                                                                                                                   |
| ------------------------------- | ------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------- |
| App 1 — `{slug}-app1`           | Mybizz's Anvil Business account                  | Development workspace. Each release is tagged here.                                                                    |
| App 2 — `master_template`       | Mybizz's Anvil Business account                  | The release: all server code, forms and UI. Its repository is the source of every client container's application code. |
| App 3 — `blank_client_template` | Mybizz's Anvil Business account                  | The client app every container runs: the startup module and the full table definitions, with App 2 as its dependency.  |
| App 4 — each client instance    | DigitalOcean App Platform and Managed PostgreSQL | One container and one database per client.                                                                             |
| App 5 — `{Product}_management`  | Mybizz's Anvil Business account                  | Creates, releases to, monitors and removes client instances through the DigitalOcean API.                              |

The demo instances (`demo.mybizz.live`, `try.mybizz.live`) stay on Mybizz's Anvil Business account.

---

## 3. The Client Instance (App 4)

### Container

- One App Platform container per client, size `apps-s-1vcpu-1gb`: 1 shared vCPU, 1 GiB memory, 150 GiB monthly bandwidth, $12 a month.
- This size can be raised for one client by a setting change, with the client staying in place.
- Region: London (`LON1`), next to Amazon SES in `eu-west-1`.

### The image

Every client container runs the same image, built once per release:

- The Anvil App Server, at the version Mybizz fixes. Every App Server upgrade is the developer's decision.
- App 3 (the client app), App 2 (`master_template`) and the `m3` theme, each linked to the App Server by its dependency ID.
- The Python packages App 2 needs, including `reportlab`.

The image is stored in DigitalOcean Container Registry (Basic plan: 5 GiB, $5 a month). Old release images are removed, keeping the last three.

### App Server settings

Each container starts the App Server with these settings, supplied as encrypted App Platform environment values:

| Setting                                                                       | Value                                                                 |
| ----------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| `database`                                                                    | The client's own database in the Managed PostgreSQL cluster, over SSL |
| `db-connection-pool-size`                                                     | 3                                                                     |
| `auto-migrate`                                                                | On                                                                    |
| `origin`                                                                      | `https://` plus the client's own domain                               |
| `disable-tls`                                                                 | On. App Platform provides the HTTPS certificate.                      |
| `secret`                                                                      | The instance's `encryption_key` (the Vault's master key)              |
| `smtp-host`, `smtp-port`, `smtp-encryption`, `smtp-username`, `smtp-password` | Amazon SES SMTP endpoint and the client's scoped SES credentials      |
| `google-*`, `microsoft-*`, `facebook-*`                                       | Mybizz's own sign-in keys, where those sign-in methods are used       |

### Container keys

The App Server keeps two keys in its data folder: `secret.key` and `anvil-live-object-key.txt`. App Platform containers keep no files across restarts. Each client's two keys are created once, at provisioning, stored as encrypted environment values, and written into the data folder by the container's start script before the App Server starts. The keys stay the same through every restart and release.

### Services the instance uses

- **Email sent:** Amazon SES through SMTP, at Mybizz's cost.
- **Email received:** Amazon SES receives each email, stores it in S3 and notifies the instance's HTTP endpoint `/_/api/email/inbound`.
- **Invoices and quotes:** PDF files built with `reportlab` on the server.
- **Files, backups and history:** the client's own Cloudflare R2 bucket, kept below 10 GB.
- **Speech-to-text:** Groq Whisper, through App 5, at Mybizz's cost.
- **Background and scheduled tasks:** run inside the App Server.
- **Heartbeats and usage reports:** sent to App 5 through the management endpoints.
- **Logs:** each container's output in DigitalOcean's log view, plus the instance's `error_log` table.

---

## 4. The Database

- One Managed PostgreSQL cluster in `LON1` holds one database per client, each with its own database user, which can reach only that client's database.
- DigitalOcean runs the patching, daily backups with 7-day retention, point-in-time recovery and SSL.
- A standby node is added when the first paying client is created. The standby takes over automatically if the main node fails.
- Each client's App Server holds at most 3 open connections. The cluster size follows the number of clients:

| Cluster memory | Connections available | Clients it carries | Price a month (with standby) |
| -------------- | --------------------- | ------------------ | ---------------------------- |
| 1 GiB          | 22                    | 7                  | $30                          |
| 2 GiB          | 47                    | 15                 | $60                          |
| 4 GiB          | 97                    | 32                 | $120                         |
| 8 GiB          | 197                   | 65                 | $240                         |
| 16 GiB         | 397                   | 132                | $480                         |

- Each client stores about 100 MB of data a year, because files go to R2. Storage stays well inside every size.
- The cluster is resized in DigitalOcean's control panel when the client count nears the size's limit. App 5 shows the count against the limit.

---

## 5. Releases

1. App 1's tagged release is pushed into App 2's repository (Step 42), and any table changes are written into App 3's table definitions.
2. The release image is built from App 2, App 3 and `m3`, and stored in the registry under the release tag.
3. A check compares App 3's new table definitions with the previous release. The release stops if any table or column is removed, renamed or changed in type. After launch, releases only add tables and columns.
4. The test client instance moves to the new image and passes its smoke test.
5. App 5's **Release** action points every client container to the new image through the DigitalOcean API. Each container restarts on the new release, and its App Server adds any new tables and columns to the client's database as it starts.
6. A staged rollout points a chosen group of clients to the new image first.
7. Rollback points the containers back to the previous release image.

---

## 6. Provisioning a New Client

App 5's **New client** action, after registration and the client's Cloudflare set-up:

1. Creates the client's database and database user in the cluster.
2. Creates the client's `encryption_key`, Bearer token and two container keys.
3. Creates the client's App Platform app from the current release image, with every setting in section 3.
4. Adds the client's domain to the app and writes its DNS records through the Cloudflare API.
5. Creates the client's R2 bucket, SES tenant, identity, receipt rule, SNS topics and scoped AWS keys, and writes every key into the instance's Vault.
6. Starts the container. The App Server builds every table in the empty database from App 3's table definitions.
7. Loads the sample data for the client's trade.

---

## 7. Client Exit

1. The client gives notice. The service runs to the end of the paid month.
2. App 5 exports all the client's data into the client's own R2 bucket.
3. App 5 removes the client's container and database. DigitalOcean's charges for them stop at removal.
4. The client keeps the R2 bucket in the client's own Cloudflare account.

---

## 8. Uptime

| Service                                | DigitalOcean's monthly commitment |
| -------------------------------------- | --------------------------------- |
| App Platform container                 | 99.95%                            |
| Managed PostgreSQL with a standby node | 99.95%                            |
| Container Registry                     | 99.95%                            |

99.95% allows about 22 minutes of downtime a month.

---

## 9. Costs

### Unit costs

| Item                                                            | Monthly cost | Basis                       |
| --------------------------------------------------------------- | ------------ | --------------------------- |
| Anvil Business account (Apps 1, 2, 3, 5 and the demo instances) | $99          | Fixed                       |
| Container Registry, Basic                                       | $5           | Fixed                       |
| Test client instance container                                  | $12          | Fixed                       |
| Client container                                                | $12          | Per client                  |
| Managed PostgreSQL cluster with standby                         | $30 to $480  | By client count (section 4) |

### Monthly totals at $99 per client

| Clients | Containers | Database | Fixed | Total cost | Revenue | Gross margin | Cost per client |
| ------- | ---------- | -------- | ----- | ---------- | ------- | ------------ | --------------- |
| 1       | $12        | $30      | $116  | $158       | $99     | −$59         | $158.00         |
| 2       | $24        | $30      | $116  | $170       | $198    | $28          | $85.00          |
| 5       | $60        | $30      | $116  | $206       | $495    | $289         | $41.20          |
| 10      | $120       | $60      | $116  | $296       | $990    | $694         | $29.60          |
| 25      | $300       | $120     | $116  | $536       | $2,475  | $1,939       | $21.44          |
| 50      | $600       | $240     | $116  | $956       | $4,950  | $3,994       | $19.12          |
| 100     | $1,200     | $480     | $116  | $1,796     | $9,900  | $8,104       | $17.96          |

Break-even is 2 clients.

### Costs outside these figures

- Amazon SES: $0.10 per 1,000 emails sent or received.
- Groq Whisper usage.
- Payment processing fees on the $99 collected from each client.
- Taxes.
- Bandwidth beyond the pooled allowance: $0.02 per GiB.

---

## 10. Commercial Terms

The client terms match DigitalOcean's terms with Mybizz: monthly billing, no contract and no lock-in.

- **Price:** $99 a month per client instance, one tier.
- **Term:** month to month. No contract and no minimum period.
- **Billing:** monthly, in advance.
- **Cancellation:** at any time, effective at the end of the paid month. No refund for part of a month.
- **Data:** on exit, the client receives all its data in its own R2 bucket.

---

## 11. Documents and PDLF Steps Affected

| Document or step                                                                   | Change                                                                                             |
| ---------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| `project-library-global/specifications-global/spec-five-app-architecture-model.md` | App 3 and App 4 roles, update model, hosting                                                       |
| `project-library-global/adr-global/adr-client-instance-architecture.md`            | Client instance runs on the Anvil App Server; schema built by the App Server                       |
| `project-library-global/adr-global/adr-dependency-update-model.md`                 | Releases through the image and App 5's Release action                                              |
| `project-library-global/specifications-global/spec-deployment.md`                  | Release, rollback, schema migration, backup, failure scenarios                                     |
| `project-library-global/specifications-global/spec-client-activation-runbook.md`   | Provisioning steps in section 6                                                                    |
| `project-library-global/adr-global/adr-client-instance-readme-five-app-system.md`  | Client instance contents                                                                           |
| `mb-3-cs-project-library/docs-local/mb-3-cs-architecture-reference.md`             | Sections 2, 4 and 5                                                                                |
| Step 7 — Create App 3                                                              | App 3 as the client app in the image                                                               |
| Step 8 — Create App 5                                                              | DigitalOcean API actions: New client, Release, Remove                                              |
| Steps 41 to 45                                                                     | Release through the image, the table-change check, the test client instance and the Release action |

**Verdict**

- The design is sound. The weak points are listed below, each with its fix.

**The risks**

1. **Anvil Cloud and the App Server can differ.** App 1 is built on Anvil Cloud, which Anvil updates continuously. The App Server is a separate release that Anvil puts out a few times a year. The App Server’s release history shows versions 1.15 (January 2026), 1.16 and 1.17 (June 2026) and 1.18 (September 2026). A feature that works in App 1 can therefore be missing or behave differently in App 4.
   - **Fix:** every release must pass the full test suite on the exact App Server image before it reaches any client. Your deployment specification already tests on the local App Server, and this makes that test a hard gate.
2. **No Anvil support for App 4.** Anvil supports its own cloud, not your self-hosted copies. A runtime bug in App 4 is Mybizz’s to solve.
   - **Fix:** pin one App Server version and upgrade only after a full test pass.
3. **One cluster, one region, one vendor.** A DigitalOcean failure in London, or a DigitalOcean account suspension, takes every client down at once.
   - **Fix:** each client’s nightly copy in the client’s own R2 bucket, plus a written rebuild procedure that restores every client in another region. Test the rebuild procedure once before launch.
4. **The release tooling is new code.** A faulty release script can hit all clients at once.
   - **Fix:** the test client instance, then a staged rollout to a few clients, then everyone. Rollback to the previous image is one action.
5. **The capacity figures are calculated, not measured.** The 1 GB memory and 3 connections per client have not yet been checked on Mybizz’s own app.
   - **Fix:** measure them on the test client instance with realistic load before the first client. If more is needed, the container size changes per client without moving the client.

**Conditions before the first paying client**

1. Full test suite passes on the App Server image.
2. Load measurement on the test client instance.
3. The rebuild procedure has been tested once.
4. The release path (test instance, staged rollout, rollback) has been run end to end once.
