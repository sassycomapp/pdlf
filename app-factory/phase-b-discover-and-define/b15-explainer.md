---
title: "b15-explainer"
doc-id: "mb-f8dcddc6"
updated: "2026-10-24"
---
# Step 15 — Engineering Review: Explainer

## What it is

Step 15 turns the agreed scope into an architecture built for Anvil, and locks it. It designs the data, the code's modules, the services, the background work and the security, then has GStack's engineering review challenge all of it. It also writes the four documents the build is checked against: the test plan, the access matrix, the threat model and the security decisions. Every later step that builds or tests the application works from what Step 15 locks.

## How it works

The step first drafts a concrete architecture into the plan, so that the review challenges a real design rather than inventing a generic one.

- The data is designed with Anvil's own `data-models` method: what the domain objects are, who owns each table, how records are created and edited, and where each rule lives. Its defaults become rules: no table is open to the browser, data rules live in model classes or server code, never in forms, and the browser never receives a column its user may not see.
- The schema is designed once, up front, so it can later grow without breaking: every core table has a metadata column, and later changes only add.
- The code is designed with Matt Pocock's `codebase-design`: the business rules sit in pure modules that can be tested on their own, behind thin server modules that handle access and storage.
- Every outside service, webhook, scheduled task, management endpoint, heartbeat and storage bucket is designed to the global standards and checked against what Anvil can actually do on the Hobby plan.
- Every process with states, such as an order or a booking, is drawn as a state machine. Where its behaviour is uncertain, Matt Pocock's `prototype` builds a small page David can click through to see whether it behaves as it should.

Then GStack's `/plan-eng-review` reviews the plan at implementation depth: architecture, code quality, tests and performance. If the plan is large, it asks David first whether a smaller arrangement would do. Every finding and every fix is put to David one at a time. PDLF answers the skill's other questions in advance.

After the review, Magnus919's `secure-software-engineering` writes the threat model: every point where data crosses from one level of trust to another, what can go wrong there, what stops it, who owns that control, and which test proves it. `security-audit-methodology` adds the security assessments the build will receive. The agent then writes the security decisions, the access matrix (every server function, form and settings tab against every role) and the test plan, with the test suite's test numbers on every flow. The architecture and data flow are drawn with Archify, after `mb-archify-scope` agrees each picture's scope with David.

Finally the agent checks everything against tests DC-01 and DC-04 to DC-08, David approves it, Sentinel reviews it at high scrutiny, and `gitleaks` checks nothing secret is in it. The step writes its ledger row and receipt, explains itself and asks David to run `/mb-close-out`.

## Why it works this way

- **Anvil first.** A review of a generic design proposes generic answers, such as a shared database or a server that keeps state. Designing with Anvil's own method first means the review improves a design that already fits the platform.
- **One plan, every decision.** The engineering review amends the same plan as the CEO review, so the concept, the scope and the architecture are read together, in one place.
- **Each review at its own depth.** Step 14 settled what to build; Step 15 settles how. David is not asked the same question twice.
- **The app keeps one access matrix and one threat model.** Every feature extends them, so the tests built from them always cover the whole application, not one feature at a time.
- **PDLF writes its own test plan.** GStack's test plan says what to test; PDLF's ties every flow to the test suite's numbered tests, so Steps 35 to 38 run exactly what was planned.
- **Nothing weak is published.** The project library is public. It records boundaries and controls; an open weakness stays in the ledger until it is fixed.
- **Global documents stay global.** A global decision that serves only this application is proposed for its own project library, because the global library depends on no application.

## What has to happen

- David drives any lifecycle prototype and accepts or corrects its behaviour.
- David answers the structure question if the plan is large, and decides every finding and fix.
- David decides every deviation from a global standard.
- David approves each diagram's scope.
- David approves the reviewed plan, the test plan, the access matrix and the threat model before the step ends.
- David decides each proposal to move a global decision into the project library.
- Only David commits, with `commit-all`, after `/mb-close-out`.
