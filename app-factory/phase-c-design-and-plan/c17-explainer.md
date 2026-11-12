---
title: "c17-explainer"
doc-id: "mb-7154c13e"
updated: "2026-11-12"
---
# Step 17 — Create Anvil Data Tables: Explainer

## What it is

Step 17 builds the application's data tables in Anvil. It is the first step of Phase C and the first step that changes the live application. It takes the data design locked at Step 16, makes sure the authoritative schema says the same thing, and then makes the app's tables in Anvil match that schema exactly.

## How it works

The authoritative schema, `authoritative-schema.md` in the project library, lists every table and column of the application. It is the one source the tables are built from. For a new application the file is empty, so the agent writes it from the data design and David approves it. For an application that already has one, the agent checks that it agrees with the data design and stops if it does not.

The agent then compares the authoritative schema with the tables the app has now, which Anvil records in `anvil.yaml`. It sorts every difference into additions, renames and removals. Renames come first and are done by David, by hand, in Anvil's Data Tables view, because a rename done by hand keeps the column's data. The agent writes David numbered instructions for each one.

After the renames, the agent writes the whole schema into `anvil.yaml` with Anvil's own `anvil-yaml` skill, checks that Anvil accepts the file, and checks it against the authoritative schema column by column. The test scanner checks the data rules: no table can be read from the browser, every table has its creation time, every core table has its metadata column, and nothing separates one client from another inside a table.

David commits the app. Anvil then sees that the tables no longer match `anvil.yaml` and shows a Resolve button in the Data Tables view. David clicks Resolve and applies each difference. The agent lists every removal by name beforehand, so David checks each one before it deletes any data. When Anvil no longer reports a mismatch, the live tables match the design. Every change is recorded in the schema migration log, which the release steps read later.

## Why it works this way

- **One source.** Building the tables from one schema, checked against the locked design, means the tables carry exactly the names and decisions Step 16 fixed.
- **Renames keep their data.** Anvil treats a rename written in `anvil.yaml` as a removal and an addition, which loses the column's data. Done by hand, the rename keeps it.
- **David changes the live tables.** An agent can write the schema but cannot change the database. Only David's Resolve applies it, so no data is deleted without his seeing it first.
- **Anvil's own skills.** `anvil-yaml` and `data-models` are Anvil's rules for its own file and its own tables, so the schema is written the way Anvil expects.
- **Proved before code.** Every later step writes code against these tables. Proving the tables match the design now stops a wrong column from being built into code.

## What has to happen

- David approves the authoritative schema when the agent has written it.
- David confirms each rename the agent cannot confirm from the migration log.
- David does each rename by hand, following the agent's instructions, then pulls the app.
- David commits the app, clicks Resolve, applies each difference and checks each removal by name.
- David confirms that the Data Tables view no longer reports a mismatch.
- Only David commits the project library, with `commit-all`, after `/mb-close-out`.
