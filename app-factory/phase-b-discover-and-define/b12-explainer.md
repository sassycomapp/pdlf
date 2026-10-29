---
title: "b12-explainer"
doc-id: "mb-634cedf5"
updated: "2026-10-29"
---
# Step 12 — Office Hours: Explainer

## What it is

Step 12 writes the concept of what is being built: the design doc. It says what problem the application or feature solves, for whom and how, inside the facts of the platform and the aspects every Mybizz application shares, with success stated so that it can be measured. David approves it, and every later step builds on it.

Step 12 runs once for each whole application (App 1, and App 5 when it is created) and once for every feature. Each run has its own design folder, `docs-local\design\{run}\`, so no concept ever overwrites another.

## How it works

Step 12 first gathers the material the concept comes from. The route depends on what already exists.

- **A new application.** The agent reads the three pre-project files and questions David with Matt Pocock's `grilling` skill. It asks a round of numbered questions, each with its recommended answer, and keeps going until every branch of the concept is settled. It looks up facts itself and asks David only for decisions. For App 5, the questions start from App 5's role in the five-app structure and from App 1's design doc.
- **An existing application.** The agent reads the whole of the business's existing documentation through GBrain, from its project context when it has one, and the code graph of the app. It treats every document as material to check, not as fact. It separates the durable concept from what merely followed from it, shows David every document that already claims to state the concept, and reports documents that name things that do not exist. David confirms or corrects the split. The application is redeveloped around its concept, not audited.
- **A feature.** The agent questions David from his description of the feature, and checks it against the application's design doc, its vocabulary, its decisions and the code it touches.

When the application follows a reference platform, such as Medusa for `mb-4-ecom`, Matt Pocock's `research` skill first checks the reference's analysis against the reference's own source code and documentation, kept in the project library's `reference-platform-local` folder, and writes its findings with a source for every claim.

The agent then writes the draft design doc in one fixed structure of thirteen sections. Its Constraints section always states the platform's facts: one app and one database per client, the server in charge of every rule, all client code public, the Hobby plan, and POPIA. Its Common Aspects section lists each of the fourteen common aspects as shared or deviating. Every success criterion has a metric, a threshold and a method, and every open question names the step that settles it. The draft is saved twice: once as the first concept, which is never changed again, and once as the working copy.

David is then asked whether to run GStack's `/office-hours` on the draft, and the recommendation is yes. `/office-hours` is given the whole draft as a fully formed plan, so it skips its interview and goes straight to challenging the premises and forcing alternatives. PDLF answers its other questions in advance; David answers only the premises and the choice of approach. The agent then rewrites the working copy from the result, in the same fixed structure.

Finally the agent checks the design doc against tests DC-01 and DC-02, David approves it, Sentinel reviews it for security, and `gitleaks` checks nothing secret is in it. The step writes its ledger row and receipt, explains itself and asks David to run `/mb-close-out`.

## Why it works this way

- **The draft comes first.** The concept never depends on whether a skill runs. `/office-hours` challenges a complete draft rather than starting from a blank page, and the first concept is always on record.
- **The first concept is never changed.** Drift can only be seen against the concept as it was first agreed.
- **One fixed structure.** Every later step and every test reads the same sections in the same order, for every application and every feature.
- **The platform's facts are written into the concept.** A concept that assumes a shared database or code hidden in the browser is wrong from its first line, and everything built on it inherits the mistake.
- **An existing application is redeveloped, not audited.** Its documents record what was decided at the time, not what is true. Keeping only the durable concept lets everything else be rebuilt properly.
- **A reference platform gives its domain, never its technology.** Its workflows are proven by real use. Its technology does not run on Anvil and would break the five-app structure.
- **`/office-hours` is told its answers.** Many of its questions are settled by PDLF's rules: sub-agents and most websites are blocked, screens come later, and Step 14 is always next. Answering them in advance means David is asked only what is his to decide.
- **One design doc in the project library.** `/office-hours` also writes a copy into the project library. Two copies would drift apart and GBrain would index both, so that copy is moved into the step folder as the record.
- **David approves here; the gate locks at Step 21.** Step 14 exists to challenge the scope, so the concept is locked only after the reviews that may change it.

## What has to happen

- David answers the interview questions and confirms the shared understanding.
- For an existing application, David confirms or corrects the split of concept and consequence.
- David runs a network grant if the reference-platform research needs a site outside Cupcake's allowlist.
- David decides whether `/office-hours` runs, and answers its questions on premises and approach.
- David approves the design doc before the step ends.
- Only David commits, with `commit-all`, after `/mb-close-out`.
