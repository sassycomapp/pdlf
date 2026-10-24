---
title: "b11-explainer"
doc-id: "mb-afda1c7f"
updated: "2026-10-24"
---
# Step 11 — Init: Explainer

## What it is

Step 11 lays the foundation of a Mybizz business, or of a new app in one, before anything about the application is designed. It makes sure the business's folders and repositories exist and are linked to GitHub, that its project library has the standard structure, that GBrain and the commit tools know about it, that the ledger has its record, and that the app can be tested. Every later step relies on that foundation without checking it again.

## How it works

The orchestrator hands Step 11 the entry record, which says how the work entered PDLF. Step 11 first checks its tools: the ledger, GBrain, Anvil's skills and command-line tool, every skill Phase B uses, and the test tools. Then it takes one of three routes.

- **A new business** (entry 02). David gives the slug, the business's name, its domain and the mode. The agent copies the project template into `C:\dev\dev-{slug}\` and sets up App 1. With David's permission it creates the public project library on GitHub, places the blank pre-project files and asks David to fill them in.
- **An application with context** (entry 03). The business already has some of its repositories. The agent checks each one, builds the code graph of each existing app, scans the public repositories for secrets, and adds only what is missing. It changes nothing that exists.
- **A new app in an existing business** (entries 07 and 08). The agent checks the business is sound, then sets up only the new app.

Setting up an app follows one pattern. David creates the app in Anvil, which also creates its repository on GitHub. In the same instructions he switches on the Users service with the sign-in settings every Mybizz app uses, and adds a `role` column to its Users table. The agent clones the app, checks it validates, and writes its `AGENTS.md` and `.gitignore`. An app that holds code (App 1 or App 5) then gets its test setup: the `tests` folders and the test suite's templates. David runs one command that writes the app's `.env` with new local keys. The agent starts the local runtime, the Anvil App Server on an empty database with a mail catcher beside it, and runs test PR-09. It proves the two Uplink connections, a `TEST_` user signing in with a second factor, and an email reaching the mail catcher. App 3 holds no code, so it gets no test setup.

For routes A and B the agent then sets up the Matt Pocock skills with PDLF's answers fixed in advance, registers the project library in GBrain, and gives David the exact lines that bring it under the commit hook and `commit-all`. Every route ends the same way: Sentinel reviews what was created for security, the health check proves the setup is sound, and the step writes its ledger row and receipt, explains itself and asks David to run `/mb-close-out`.

## Why it works this way

- **One end for every route.** However a business enters PDLF, it leaves Step 11 having passed the same health check, so every later step can trust the same foundation.
- **The tools are checked first.** A missing skill or an unreachable ledger found at Step 11 costs nothing; found halfway through a review, it costs the review.
- **Anvil creates each app's repository.** An Anvil app's code repository must come from Anvil, or Anvil cannot keep it in step. So David creates the app, and the agent only clones it.
- **David switches on the Users service.** Its settings live in `anvil.yaml`, which no agent writes, and its Users table is part of the schema, which only David changes. Every Mybizz app signs in the same way, so the settings are fixed from the start.
- **The test setup comes first.** Every test from Step 35 on depends on the local runtime and the two Uplink connections. PR-09 proves them once, at the start, so a broken test environment is never mistaken for broken code.
- **David writes `.env`.** It holds the keys. No agent reads or writes it; `ts_local.sh` passes the keys to the runtime and the tests without showing them.
- **The template is copied without document identities.** The commit hook gives every document a permanent identity. If the template's identities were copied, every project would share them and the hook would confuse one project's documents with another's.
- **Tickets stay in the project library.** Tickets are documentation, so they live with the business's documents, never in an app's code.
- **Nothing existing is changed without permission.** An existing application's material is David's. Step 11 reports what is wrong; David decides.
- **Sentinel reviews Step 11.** The repositories are public, so a secret that slips in at the start would be published with everything after it.

## What has to happen

- David creates each app in Anvil, connects it to GitHub, switches on its Users service and adds the `role` column when asked.
- David runs the command that writes the app's `.env`, and confirms.
- David approves the creation of the project library on GitHub.
- David adds the project library to the commit tools with the lines the agent gives him, and confirms.
- David fills in the three pre-project files before Step 12.
- Only David commits, with `commit-all`, after `/mb-close-out`.
