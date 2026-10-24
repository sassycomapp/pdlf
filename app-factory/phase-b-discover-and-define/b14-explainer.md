---
title: "b14-explainer"
doc-id: "mb-0111675e"
updated: "2026-10-24"
---
# Step 14 — CEO Review: Explainer

## What it is

Step 14 settles how far the application, or the feature, goes. It challenges the concept David approved at Step 12, and lets David choose whether to widen the scope, hold it or cut it. Around the scope it settles the things that follow from it: what data the application holds and how each kind is protected, which laws apply, what the business must keep secure, how a client leaves with their data, and whether a typical client fits on Anvil's Hobby plan. It also names what must be tested, and why. The result is the reviewed plan that Step 15 turns into an architecture.

## How it works

The step works in the same design doc Step 12 wrote. GStack's reviews are built to amend one plan file and keep their report at its end, so the concept and its reviews live in one document.

First, Magnus919's `secure-software-engineering` skill drafts five new sections: the Data Inventory, the Regulatory Position, the Security Requirements, the Client Exit and the Hobby Fit. Every kind of data gets an owner, its readers and writers, one of four protection levels (Public, Internal, Personal, Restricted) and a retention period.

Then GStack's `/plan-ceo-review` reviews the whole plan, those sections included. It challenges the premise, recommends a scope mode, and David chooses one: expansion, selective expansion, hold scope or reduction. The skill then works through its review sections at the level of strategy, putting every finding and every proposed addition, cut or deferral to David one at a time. PDLF answers its other questions in advance.

While the review runs, the agent checks every addition David accepts against Anvil's own documentation and skills, so the plan never promises something Anvil cannot do. Any proposal that would break a global standard is named to David. The standard holds unless he approves a deviation, and an approved deviation is written as a decision record, with its reason, in the project's `adr-local` folder.

After the review, the agent adds two sections: Scope, with the goals and non-goals, and What Must Be Tested, with every critical flow, role and edge case and the reason each matters. It checks the plan against tests DC-03 and DC-01. David approves the reviewed plan, Sentinel reviews it for security, and `gitleaks` checks nothing secret is in it. The step writes its ledger row and receipt, explains itself and asks David to run `/mb-close-out`.

## Why it works this way

- **One plan, amended in place.** One document carries the concept and every decision made about it. Two documents would drift apart, and later steps would not know which to trust.
- **Security, data and law come before the review.** A wider scope brings more data and more law. Drafting these first means the review weighs them with the scope, instead of discovering them afterwards.
- **Strategy here, implementation at Step 15.** Both reviews cover similar ground. Keeping this one at the level of strategy means David is never asked the same question twice.
- **Every choice is David's, one at a time.** The scope is the biggest commitment in the build. A batch of findings is where a tired reviewer starts agreeing without reading.
- **No to-do file.** PDLF keeps one register, the ledger. A deferred capability is written into the plan with its reason, and it comes back later as a feature when David wants it.
- **Global standards hold unless David decides.** Every Mybizz application shares one structure. A change for one application is a recorded decision, never a quiet drift.
- **Anvil is checked as the scope grows.** A promise Anvil cannot keep costs nothing to drop now and a great deal to discover at Step 35.

## What has to happen

- David chooses the scope mode.
- David decides every finding, addition, cut and deferral the review raises.
- David decides every deviation from a global standard.
- David approves the reviewed plan before the step ends.
- Only David commits, with `commit-all`, after `/mb-close-out`.
