---

title: "Alternatives to Anvil for App 4"
doc-id: "mb-76627bd0"
updated: "2026-11-07"

---

# Alternatives to Anvil for App 4

Is anvil.works open source and what license does it have? Is it an MIT license or Apache 2.0 license? Which license does it have?

Anvil ([anvil.works](https://anvil.works/open-source)) features an open-source App Server and Runtime engine.

GitHub

It does not use either the MIT or Apache 2.0 license; instead, it is released under the **GNU Affero General Public License v3.0 (AGPLv3)** with an explicit exception allowing users to host non-open-source applications.

I've developed my application in anvil.works. Can I move my application using their runtime to a different server?

Yes, you can export your application from the cloud editor and run it on any server or hardware using the open-source **Anvil App Server** runtime engine.

Anvil Works

If I was to move my application using Anvil's runtime service to a different hosting platform, what Anvil.works services would I need to replace?

When moving an Anvil application from their managed cloud to a self-hosted environment using the **Anvil App Server** runtime, you take over the server infrastructure that Anvil's cloud previously managed automatically.

Depending on how much your application relies on Anvil's built-in managed platform services, you will need to replace or provision substitutes for the following components:

### 1. Database Backend (Anvil Data Tables)

- **What Anvil provides:** A built-in, managed PostgreSQL-backed database with a visual GUI editor and built-in Python API (`anvil.server.db`).

- **What you need to replace it with:** The open-source Anvil App Server natively supports connecting to external databases (such as a standalone PostgreSQL or MySQL instance) using standard connection strings. You will need to provision and manage your own database server, map your data tables, and handle backups.

### 2. File Storage

- **What Anvil provides:** Managed file storage for media files and user uploads handled via Anvil's data tables or media objects.

- **What you need to replace it with:** If your app handles file uploads, you must configure the app server to store files locally on disk or redirect storage integrations to an object storage provider (such as AWS S3, Cloudflare R2, or a compatible bucket service).

### 3. Background Tasks & Scheduler

- **What Anvil provides:** Anvil's cloud automatically handles asynchronous background tasks and scheduled routines.

- **What you need to replace it with:** The open-source Anvil App Server includes background task handling, but you must ensure your host server has sufficient persistent uptime, process management (e.g., using `systemd` or Docker), and resource allocation to handle concurrent jobs without crashing.

### 4. User Authentication & Session Management

- **What Anvil provides:** Out-of-the-box user authentication services (Email/Password, Google, Enterprise SSO, multi-factor flows) with managed user tables.

- **What you need to replace it with:** While Anvil's built-in authentication modules still function in the open-source runtime, you are responsible for securing the underlying database where user credentials and tokens reside, configuring mail servers for password resets, and managing SSL/TLS certificates.

### 5. Email Sending and Receiving APIs

- **What Anvil provides:** Built-in email utilities (`anvil.email.send`) managed via Anvil's outbound mail infrastructure.

- **What you need to replace it with:** To send emails from a self-hosted instance, you must configure an external SMTP relay or transactional email provider (such as SendGrid, Mailgun, or Amazon SES) and supply the SMTP environment variables to your runtime.

### 6. SSL/TLS Certificates and Domain Routing

- **What Anvil provides:** Automated HTTPS certificate provisioning and custom domain routing.

- **What you need to replace it with:** You will need to sit your self-hosted Anvil App Server behind a reverse proxy (such as Nginx, Caddy, or a cloud load balancer) to handle SSL termination (e.g., via Let's Encrypt), domain mapping, and traffic routing.

Want to know how to configure the Anvil App Server with an external database and reverse proxy?

Yes

The measure that I am evaluating against is Anvil.works $99 per month for a business account. The six points which you listed in your last response do seem to be great value for the $99 per month.

I'm trying to reduce my total cost of an account to under $50 per month, which would include a full replacement for the above six points as well as the web application hosting. Are there any real alternatives which fully match the criteria?

Please do not propose partial solutions. I'm looking for full replacement only Even if the full replacement requires using several services, but the overall cost must not come to more than $50 per month. And I will need to fully replace all six of those features, services, as well as the web app hosting and any other services which are dependent on anvil.works and that will need to be replaced.

To completely replace Anvil.works (including web application hosting, data storage, auth, background processing, email, and SSL) for **under $50 per month**, two primary paths exist:

1. **Option A: Managed Cloud PaaS** (Zero server maintenance)

2. **Option B: Single VPS + Open-Source PaaS Engine** (Maximum performance per dollar)

Both paths fully cover all six core dependencies identified in the previous response.

### Option A: Fully Managed Cloud PaaS (Render or DigitalOcean)

*Cost: ~$18 – $28 / month total*

This setup replicates the zero-server-maintenance experience of Anvil Cloud without requiring manual OS patching or container orchestration.

| Anvil Service              | Managed Replacement Service                                                   | Monthly Cost                     |
| -------------------------- | ----------------------------------------------------------------------------- | -------------------------------- |
| **Web App Hosting**        | **Render Web Service** (512MB RAM) or **DO App Platform**                     | $5.00 – $7.00                    |
| **1. Database**            | **Managed PostgreSQL** (Render / DigitalOcean Starter instance)               | $6.00 – $15.00                   |
| **2. File Storage**        | **Cloudflare R2** or **AWS S3** (10GB storage + transfers)                    | ~$0.00 (R2 has a 10GB free tier) |
| **3. Workers / Scheduler** | Background worker process on App Server or Cron job container                 | Included in App compute / $5.00  |
| **4. Auth & Sessions**     | **Supabase Auth** / **Clerk** (Free Tiers: 50k MAU)                           | $0.00                            |
| **5. Outbound Mail**       | **SendGrid**, **Resend**, or **Mailgun** (Free Tiers: 3,000–3,0000 emails/mo) | $0.00                            |
| **6. SSL & Routing**       | Built-in SSL (Let's Encrypt / Cloudflare)                                     | $0.00                            |
| **Total Estimated Spend**  |                                                                               | **~$18.00 – $28.00 / mo**        |

### Option B: Single VPS + Open-Source PaaS (Dokploy / Coolify / CapRover)

*Cost: ~$10 – $24 / month total*

Dokploy

Provisioning a single Virtual Private Server (VPS) on **Hetzner**, **DigitalOcean**, or **Linode** and running an open-source orchestration panel such as **Dokploy** or **Coolify** allows hosting the **Anvil App Server runtime**, database, background workers, and reverse proxy on one isolated server.

Dokploy

```
┌────────────────────────────────────────────────────────┐
│                   SINGLE VPS INSTANCE                  │
│  ┌──────────────────────────────────────────────────┐  │
│  │ Traefik / Nginx (Automated SSL & Reverse Proxy)   │  │
│  └──────────────────────────┬───────────────────────┘  │
│                             │                          │
│        ┌────────────────────┴──────────────────┐       │
│        ▼                                       ▼       │
│  ┌──────────────┐                       ┌───────────┐  │
│  │ Anvil App    │◄─── Internal Net ────►│ Postgres  │  │
│  │ Server       │                       │ DB        │  │
│  └──────────────┘                       └───────────┘  │
└────────────────────────────────────────────────────────┘
```

| Anvil Service                     | Self-Hosted Replacement Stack                                      | Monthly Cost             |
| --------------------------------- | ------------------------------------------------------------------ | ------------------------ |
| **Web App Hosting + VPS Compute** | **Hetzner CX23 / CX33** (2–4 vCPU, 4–8GB RAM) or **DO Droplet**    | $6.00 – $14.00           |
| **PaaS Control Panel**            | **Dokploy** or **Coolify** (Open Source)                           | $0.00                    |
| **1. Database**                   | Containerized **PostgreSQL** running locally on the VPS            | $0.00 (uses VPS RAM/CPU) |
| **2. File Storage**               | **Cloudflare R2** bucket or VPS local volume storage               | $0.00                    |
| **3. Workers / Scheduler**        | Background processes managed natively inside the Anvil container   | $0.00                    |
| **4. Auth & Sessions**            | Native Anvil Auth using the local Postgres DB                      | $0.00                    |
| **5. Outbound Mail**              | **SendGrid** / **Resend** (API/SMTP Relay on free tier)            | $0.00                    |
| **6. SSL & Routing**              | Automated SSL termination via Traefik (Built into Dokploy/Coolify) | $0.00                    |
| **Total Estimated Spend**         |                                                                    | **~$6.00 – $14.00 / mo** |

### Key Technical Trade-Offs

1. **Setup Effort:**
   
   - **Managed Cloud (Option A)** requires setting up external provider credentials (e.g., SendGrid API keys, Supabase credentials) in environment variables.
   
   - **VPS (Option B)** requires a one-line curl command to install Dokploy/Coolify on a bare Ubuntu server. The control panel then handles Git deployments, database creation, container management, and automatic SSL provisioning via a browser GUI.
     
     Dokploy

2. **Database Resilience:**
   
   - In Option A, database backups, replication, and uptime are fully automated by the cloud provider.
   
   - In Option B, cron jobs must be set up to dump the local Postgres database to an off-site object storage bucket (e.g., Cloudflare R2) regularly.

Would you like a step-by-step deployment guide for Dokploy on a single VPS?

Yes

Option A seems to be the least technically challenging solution.

Add Automatic Git integration to the List of services provided by Anvil that would need to be replaced.

Now consider the usage limits and constraints provided by anvil on their business platform and compare that to what is provided by the solutions in option A

### Updated Service List (7 Dependencies to Replace)

1. **Web App Hosting & Compute**

2. **Database Backend** (Anvil Data Tables)

3. **File Storage**

4. **Workers & Task Scheduler**

5. **Auth & Session Management**

6. **Outbound Mail / SMTP**

7. **Automated Git Deployment & CI/CD Pipelines** (Anvil automatically deploys when you push to their hosted Git repository or commit in the web editor)

### Anvil Business Plan Limits vs. Option A (Render / Managed Cloud PaaS)

Evaluating Anvil's $99/month Business Tier against a fully managed PaaS setup (such as Render or DigitalOcean App Platform) reveals how constraints and resource allocations shift under the $50/month target.

| Resource / Feature       | Anvil Business Plan ($99/mo)                                                                   | Option A: Render Managed Stack (~$18–$28/mo)                                        | Comparison & Impact                                                                                                            |
| ------------------------ | ---------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| **Compute & CPU/RAM**    | Shared multi-tenant environment. Dedicated compute requires custom Enterprise pricing.         | Dedicated 0.5 vCPU / 512 MB to 1 vCPU / 2 GB containers ($7–$25/mo).                | **Option A Wins.** You get isolated, predictable memory and CPU allocations instead of shared compute bursts.                  |
| **Execution Time Out**   | **30 seconds** per request/function call. Longer processes must use Background Tasks.          | **100 seconds** (Web) to **Unlimited** (Background Workers).                        | **Option A Wins.** Higher request execution limits remove the strict 30-second cap for processing operations.                  |
| **Database Storage**     | **100 MB** included in data tables (50,000 row cap on lower tiers, extra storage costs apply). | **1 GB – 10 GB** included ($6–$15/mo managed Postgres).                             | **Option A Wins.** Vastly more database capacity for a fraction of the cost ($0.30/GB overage vs. proprietary table upgrades). |
| **File Storage**         | Shared static file storage limits tied to account disk space.                                  | **10 GB Free** via Cloudflare R2 / S3 ($0.00/mo).                                   | **Option A Wins.** Decouples file uploads from application memory and database space.                                          |
| **Git Integration**      | Built-in Git engine. Pushing code directly to Anvil builds and updates the live environment.   | Native GitHub/GitLab integration. Auto-deploys on `git push` to your `main` branch. | **Tie.** Both provide automated continuous deployment upon pushing commits.                                                    |
| **User Accounts / Auth** | Unlimited users via `anvil.users` module.                                                      | **50,000 Monthly Active Users (MAU)** free via Supabase Auth or Clerk.              | **Tie.** Free tiers of modern auth providers far exceed small-to-medium app requirements.                                      |
| **Outbound Email**       | Managed via Anvil SMTP limits (throttled on high-volume bursts).                               | **3,000 – 30,000 emails/mo Free** (SendGrid / Resend / Mailgun API).                | **Tie / Option A Wins.** Provides custom domain authentication (DKIM/SPF) directly with mail providers.                        |
| **Outbound Bandwidth**   | Included in shared plan (subject to fair use).                                                 | **5 GB to 50 GB included/mo** ($0.15/GB overage).                                   | **Slight Advantage Anvil** for ultra-high traffic apps, though 5–50 GB easily handles typical SaaS usage.                      |

### Bottom Line Comparison

- **Cost Savings:** Option A cuts your software bill from **$99/mo to ~$18–$28/mo**, saving over **$850 per year**.

- **Resource Bounds:** Anvil’s $99 plan caps data table storage at 100 MB and enforces a 30-second timeout. Option A provides a dedicated database (1 GB+ storage) and removes the 30-second constraint.
  
  anvil.works

- **Maintenance Trade-off:** Option A requires managing configuration files (`Dockerfile` or Render build environment variables) and wiring services together (DB connection string, SendGrid API keys), whereas Anvil handles wiring out of the box.

List the complete itemized table of costs that I will be facing when using when using option A. Hideen and forgotten costs are what will break the business

Here is the complete, itemized breakdown of costs for replacing Anvil.works with a managed PaaS stack (Option A), including core infrastructure, supporting operations, and the hidden traps that push small hosting bills over budget.

### Core Infrastructure & Essential Replacements

| Anvil Feature Replaced              | Provider / Service Choice                         | Monthly Base Cost        | Billing Basis & Inclusions                                                   | Potential Overages & Hidden Escalators                                                                             |
| ----------------------------------- | ------------------------------------------------- | ------------------------ | ---------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| **1. Web App Compute**              | **Render Starter** or **DO App Platform Starter** | **$5.00 – $7.00**        | 512MB–1GB RAM, 0.5 vCPU; always-on instance.                                 | CPU/RAM autoscaling bursts; upgrading to 2GB RAM container adds **+$18–$20/mo**.                                   |
| **2. Database (Anvil Data Tables)** | **Render Basic Postgres** or **DigitalOcean DB**  | **$6.00 – $15.00**       | Includes ~1GB–10GB disk space & automated daily backups.                     | Database storage past 1GB costs **$0.30/GB/mo** on Render. IOPS limits forces instance tier-up under heavy writes. |
| **3. File Storage**                 | **Cloudflare R2**                                 | **$0.00**                | **Free Tier:** 10 GB storage, 1M Class A writes, 10M Class B reads/mo.       | **Zero Egress Fees**. Storage beyond 10GB is **$0.015/GB/mo**.                                                     |
| **4. Background Workers**           | **App Server Process** or **Render Worker**       | **$0.00 – $7.00**        | Included if run in same app container; separate worker instance costs $7/mo. | Long-running tasks crash 512MB RAM containers; requires memory headroom.                                           |
| **5. Auth & User Management**       | **Supabase Auth** or **Clerk**                    | **$0.00**                | **Free Tier:** Up to 50,000 Monthly Active Users (MAUs).                     | B2B Enterprise SSO features (SAML/OIDC) trigger tier jumps to **+$25–$99/mo**.                                     |
| **6. Outbound Mail / SMTP**         | **Resend**, **SendGrid**, or **Mailgun**          | **$0.00**                | **Free Tier:** 3,000 to 30,000 outbound emails/mo.                           | Dedicated IP addresses (for deliverability) cost **+$30–$40/mo**. Volume overages past free caps.                  |
| **7. Git CI/CD & Deployments**      | **GitHub Actions** + PaaS Hooks                   | **$0.00**                | **Free Tier:** 2,000 build minutes/mo on public/private repos.               | Exceeding Render's build pipeline limits adds **$5 per 1,000 build minutes**.                                      |
| **8. SSL / Domain Routing**         | **Let's Encrypt / Cloudflare**                    | **$0.00**                | Unlimited SSL certificates and DNS routing.                                  | Custom domains past account baseline limit cost **$0.25/domain/mo**.                                               |
| **CORE INFRASTRUCTURE TOTAL**       |                                                   | **$11.00 – $29.00 / mo** |                                                                              |                                                                                                                    |

### Hidden Operational Costs (Often Forgotten)

| Forgotten Operational Need                  | Provider / Service Choice                  | Monthly Cost                          | Why It Is Essential & How It Fails You If Ignored                                                                                                                                                                                        |
| ------------------------------------------- | ------------------------------------------ | ------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Application Performance & Error Logging** | **Sentry (Developer Tier)** or **Logtail** | **$0.00** *(Free up to 5K events/mo)* | Anvil automatically surfaces Python tracebacks in the cloud console. Raw PaaS instances clear logs on reboot; without a log aggregator, user-reported bugs leave zero trail. Paid logs add **+$15–$26/mo**.                              |
| **Off-Site Database Backups**               | **R2 / S3 Storage + Cron**                 | **$0.00 – $1.00**                     | Managed DBs back up locally, but point-in-time restoration or Disaster Recovery export requires automated snapshotting to secondary cloud buckets.                                                                                       |
| **Staging / Preview Environments**          | **PaaS Preview Instances**                 | **$0.00 – $13.00**                    | Anvil provides isolated published vs. dev environments out-of-the-box. Running a 1:1 staging stack (web + database) on PaaS **doubles your compute costs**. *(Use transient preview environments on free tiers to avoid extra billing)*. |
| **Transactional Outbound Traffic (Egress)** | PaaS Bandwidth Allowance                   | **$0.00 – $5.00**                     | Free bandwidth allowances range from 5GB (Render Hobby) to 50GB (DO App Platform). Bandwidth overages run **$0.15 per GB** on Render or **$0.01 per GB** on DigitalOcean.                                                                |
| **Domain Name Registration & DNS**          | Registrar (Cloudflare / Namecheap)         | **~$1.00** *($12/year)*               | Required for custom domain deployment and setting up SPF/DKIM mail records.                                                                                                                                                              |
| **TOTAL WITH ALL HIDDEN COSTS**             |                                            | **$12.00 – $48.00 / mo**              | *(Leaves a safety buffer under the $50 cap)*                                                                                                                                                                                             |

### 3 Hidden "Traps" That Can Break the $50 Budget

1. **The Memory Threshold (RAM Spikes):** Anvil isolates app server memory on their cluster. In a $7/mo PaaS container with only 512MB RAM, a memory-heavy Python process (such as parsing large file uploads or running data analysis libraries) will trigger an **Out-Of-Memory (OOM) Kill**, crashing your app server. Scaling up compute to 2GB RAM jumps costs to **~$25/mo** per container.
   
   Temps

2. **Transactional Email Deliverability:** While email APIs (SendGrid/Resend) are free up to thousands of messages per month, sending transactional app emails from a new shared IP address can hit spam filters. If your transactional emails land in spam, purchasing a **Dedicated Outbound IP** costs **$30–$40/month**, which immediately eats up your budget savings.

3. **Staging Environment Multiplication:** If you spin up an active staging database and staging app server alongside your production app, you double your baseline database and container charges ($13 prod + $13 staging = $26/mo). Keep staging databases short-lived or use local docker-compose environments during development.

Lets add real context so that we can discuss closer to the actual truth.

I have a saas business called mybizz. Mybizz onsista of a 5 app structure: app1: the dev app which creates app2. App2: (master template) the dependency app to app4. App3: the template for creating new app4 instances. App4: the client instances (there can be up to 100). App5: mybizz mamagement app where I managage the client instances (registrations, accounting, etc). Each client instance is a separate anvil business account. Apps 1,2,3,5 are on a single anvil business account. Mybizz owns all tje anvil accounts even the individual client instance accounts. Clients are all on a month to month, there are no yearly accounts. Mybizz offers 1 account tier at 1 rate. AWS-SES provides all smtp at mybizz cost, so no additional smtp on-costs to clients. R2 bucket accounts are in the individual client names but are maintained below 10Gb so are free. Mybiz provides grok whisper at mybizz cost.

The I am trying to provide the mybizz service for under $100 permonth to the client but that is not possible with Anvil, therefor I am looking at alternative arrangements.

1 option is to provide the mybizz service to clients at $150 pm which obviates all the additional stress of teying to replace anvil but market position then becomes the crucial pivot

The competing pivots are the Anvil $99pm/ ease of use (with constraints) vs. Option A with its pros and cons and potentially equally expensive cost to mybizz and the high maintenance burden

This is the dilemma

Having explicit context completely changes the equation.

Your structural constraint isn't just "hosting a web app." Your architecture requires **multi-tenant single isolation**:

- **1 Master Account** hosting Apps 1, 2, 3, and 5.

- **Up to 100 isolated App4 instances**, each needing its own independent database/data boundary.

When you look at this architecture through the lens of scaling up to 100 clients, the math and the operational mechanics reveal why your dilemma exists—and why **Option A (Re-platforming to generic PaaS)** is actually the wrong alternative to evaluate against Anvil Cloud.

### The Anvil Math (Why Anvil Cloud breaks at <$100/mo)

If every App4 client instance requires a separate Anvil Business Account ($99/mo):

Fixed Hosting Cost per Client=$99/month

If you sell MyBizz at **$100/mo**, your gross profit per client is **$1.00** before paying for AWS-SES, Grok Whisper API calls, or your central management account (Apps 1, 2, 3, 5).

- **At $150/mo on Anvil Cloud:** You make **~$51/mo margin per client**, but you face high market friction charging $150/mo for standard SMB SaaS.

- **At $99/mo on Anvil Cloud:** The business operates at a structural loss.

### Why "Option A" (Generic PaaS/Re-platforming) is a Trap

Rewriting or porting a 5-app Anvil architecture to standard frameworks (React, FastAPI, Supabase, Render) to cut hosting costs introduces massive friction:

1. **Re-architecture Cost:** Rebuilding Python-in-browser forms, server modules, dependency linkages (App2 → App4), and the management orchestration (App5) into native code will cost thousands of dollars or months of dev work.

2. **Multi-Tenant Operations:** Provisioning 100 separate database schemas, 100 auth instances, and 100 app deployment pipelines across services like Render or Supabase requires writing complex custom infrastructure code (DevOps).

### Option C: The Real Alternative (Self-Hosted Anvil App Server on VPS)

Instead of choosing between **$99/client Anvil Cloud** vs. **Re-building the app for generic PaaS (Option A)**, the true comparison is **Anvil Cloud vs. Open-Source Anvil App Server**.

Anvil Works

Because Anvil’s runtime engine is open-source (AGPLv3 with hosting exceptions), you can deploy **App4 instances natively using the Anvil App Server** on standard cloud servers.

Anvil Works

```
                     ┌────────────────────────────────────────────────────────┐
                     │                 $20 - $40 / mo VPS                     │
                     │             (e.g. Hetzner / DigitalOcean)              │
                     │                                                        │
                     │  ┌──────────────────────────────────────────────────┐  │
                     │  │        Caddy / Nginx Reverse Proxy (SSL)         │  │
                     │  └──────────┬──────────────────┬─────────────────┬──┘  │
                     │             │                  │                 │     │
                     │        Port 3001          Port 3002         Port 300N  │
                     │             ▼                  ▼                 ▼     │
                     │       ┌──────────┐       ┌──────────┐      ┌──────────┐│
                     │       │ App4     │       │ App4     │      │ App4     ││
                     │       │ Client 1 │       │ Client 2 │  ... │ Client N ││
                     │       └────┬─────┘       └────┬─────┘      └────┬─────┘│
                     │            │                  │                 │      │
                     │            ▼                  ▼                 ▼      │
                     │       ┌──────────┐       ┌──────────┐      ┌──────────┐│
                     │       │ Postgres │       │ Postgres │      │ Postgres ││
                     │       │ DB 1     │       │ DB 2     │      │ DB N     ││
                     │       └──────────┘       └──────────┘      └──────────┘│
                     └────────────────────────────────────────────────────────┘
```

#### How it works for MyBizz:

1. **Zero Re-writing:** You keep your entire Python code base, forms, dependencies, and business logic intact.

2. **Multi-App Density:** A single 8GB/4-vCPU VPS ($24/mo) can easily run 20 to 30 idle/lightly active `anvil-app-server` instances inside Docker containers.

3. **App5 Orchestration:** When a new client registers in App5, your system triggers a script that:
   
   - Spins up a new Docker container running `anvil-app-server --app App4_Template` on a new port.
   
   - Provisions an isolated PostgreSQL database for that client.
   
   - Binds the domain/subdomain automatically via Caddy/Traefik API.

#### The Unit Economics of Option C:

- **Cost per 25 Clients:** ~$30/mo (VPS compute + DB storage).

- **Cost per Client:** **~$1.20 / month** (versus $99/mo on Anvil Cloud).

- **At $99/mo Client Price:** Your gross margin is **~97%** instead of 1%.

### Comparing the Strategic Options

| Feature / Pivot           | Plan A: Anvil Cloud ($150/mo)  | Plan B: Generic PaaS (Option A) | Plan C: Self-Hosted Anvil App Server |
| ------------------------- | ------------------------------ | ------------------------------- | ------------------------------------ |
| **Client Pricing**        | $150 / month                   | <$100 / month                   | **<$100 / month**                    |
| **Hosting Cost / Client** | $99.00 / month                 | ~$5.00 / month                  | **~$1.20 / month**                   |
| **Code Base Status**      | Keep existing Anvil code       | Complete Rewrite required       | **Keep existing Anvil code**         |
| **DevOps Burden**         | Zero                           | High                            | Medium (Containerized deployment)    |
| **Database Isolation**    | Native Anvil Tables            | Custom Schema Setup             | **Isolated Postgres per instance**   |
| **Market Friction**       | **High** ($150/mo price point) | Low                             | **Low** ($99/mo sweet spot)          |

### Strategic Recommendation

1. **Avoid the $150/mo price jump if it creates sales friction.** If your target market prefers an under-$100 price point, forcing $150/mo just to cover Anvil's per-account license fee puts product-market fit at risk.

2. **Do not rewrite for generic PaaS.** Rewriting Python/Anvil code to React/FastAPI just to reduce server fees wastes capital and time.

3. **Containerize App4 via Open-Source Anvil Runtime.** Keep Apps 1, 2, 3, and 5 hosted on your single Anvil Business Account ($99/mo flat). Use your dev app (App1) to generate client builds, but deploy the resulting App4 instances onto your own VPS infrastructure using Docker + `anvil-app-server`.
