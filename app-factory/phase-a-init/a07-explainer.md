---
title: "a07-explainer"
doc-id: "mb-e7e98a42"
updated: "2026-10-29"
---
# Step 7 — Create App 3: Explainer

## What it is

Step 7 is the entry point `create-client-template`. Its job: App 3, `blank_client_template`, entered into PDLF for a business whose existing apps are shown healthy, so that Step 11 sets it up; Steps 12 to 16 do not run for it, because it holds only App 1's schema, one startup module and its dependency on App 2.

## How it works

David opens OpenCode in the business folder and runs `/pdlf-init`, then chooses this entry. The orchestrator runs the health check, asks its questions, and writes the entry record. The run continues at Step 11, route C.

## Why it works this way

- **No design steps.** App 3 is built from App 1's schema; there is nothing in it to scope or review.
- **It only records.** An entry point asks and writes the entry record; every change to the business is made by the steps it joins, where it is checked.

## What has to happen

- David opens OpenCode in the business folder and runs `/pdlf-init`.
- David answers the entry's questions.
- David runs `/mb-close-out` when the entry stops, and says "continue".
