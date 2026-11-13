---
title: "e35-explainer"
doc-id: "mb-7febe5a3"
updated: "2026-11-13"
---
# Step 35 — Build: Explainer

## What it is

Step 35 builds one feature of the application, from its ticket, and proves it works. It runs once for every ticket, in build order.

## How it works

The step follows the UI production method. First, the server code: each behaviour the ticket names is built test-first, using Matt Pocock's `tdd` and Anvil's own skills for server code, client modules and data, into the empty functions planned at Step 31. It is tested on its own, then together with the app on the local runtime. Claude reviews it, and David commits it.

Then the forms: `mb-form-builder` builds each of the ticket's forms exactly as its approved screen requirement says, following Anvil's `client-forms` skill, and removes the old forms it replaces. Claude reviews them, and David opens each form in Anvil to see it is right. Anvil's own agent then fills in only the empty event handlers, as each form's spec sheet says, and checks its own work. Claude confirms that nothing else changed.

Finally, any old code this ticket was due to replace is cleared, and David tries every flow in the browser, on desktop and phone, with test data only. He signs the feature off. Sentinel reviews the feature's code for security.

## Why it works this way

- **Code first, forms second.** A form is wired to server code that already works, so a fault is found in one place.
- **Built as approved.** Each form comes straight from the screen requirement David approved.
- **No agent judges itself.** OpenCode builds, Anvil's agent wires, Claude reviews and David signs off.

## What has to happen

- David passes each review package to Claude and returns Claude's findings.
- David commits, opens each form in Anvil, gives Anvil's agent its wiring task, runs the browser check and signs the feature off.
- Only David commits, with `commit-all` and `gcp`.
