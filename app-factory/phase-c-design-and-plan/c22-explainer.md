---
title: "c22-explainer"
doc-id: "mb-f982342e"
updated: "2026-11-12"
---
# Step 22 — Screen Requirements: Explainer

## What it is

Step 22 writes a screen requirement for every form the tickets name. A screen requirement is the full design of one form, in words and tables: what is on it, which theme component shows each part and why, what data it shows, what each action does, who may use it and what every text says.

## How it works

Before writing anything, the agent reads the whole of `m3-custom-theme`'s component documentation, all 49 components. Then, ticket by ticket, it writes each form's screen requirement from the model in the project library's `ui` folder. For every element of a screen it names the theme component that serves that element best, and says why that component is better than the others that could do the job. A plain Anvil component is used only where the theme has nothing for the purpose.

Each requirement names the data from the authoritative schema, the server function each action calls, the scope of every role, every text as a phrase key with its English wording, the help video for each process, and the user flows the form belongs to. Where the documents do not settle something, the agent asks David with its recommended answer. Every requirement is written as a draft; David approves them at Step 26.

## Why it works this way

- **Design before build.** `mb-form-builder` builds each form exactly as its approved requirement says, so the design decisions are made here, where David can see and approve them.
- **The best component, not the first.** Reading the whole theme first, and justifying each choice against the alternatives, makes full use of the theme on every screen.
- **Nothing guessed.** Every component, property, column and function is taken from the document that defines it, so the builder never invents one.

## What has to happen

- David answers the questions the documents do not settle.
- Only David commits the project library, with `commit-all`, after `/mb-close-out`.
