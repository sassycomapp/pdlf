---
title: "c23-explainer"
doc-id: "mb-2c1488ad"
updated: "2026-11-12"
---
# Step 23 — Design Review: Explainer

## What it is

Step 23 reviews every screen requirement and `DESIGN.md` before David approves them. It records every finding with its severity; it changes nothing. Step 26 makes the corrections.

## How it works

GStack's `/plan-design-review` rates the screen designs on usability and lists each gap it finds. The agent then runs three checks of its own on every screen requirement. The theme-usage check compares each element with the whole of `m3-custom-theme`'s component set: wherever a better-fitting component exists, that is a high-severity finding, naming the better component. The accessibility check applies the rules for keyboard use, contrast, names and touch targets. The controls check confirms the tooltips switch, the help videos menu and the dashboard button are available.

Every finding names its screen, its element, the proposed correction and its severity: high, medium or low.

## Why it works this way

- **Challenge before approval.** David approves screens that have already been reviewed and corrected, not first drafts.
- **Full use of the theme is enforced.** The theme-usage check catches every plain component chosen where a better one exists, and rates it high so that it must be corrected.
- **Findings, not silent fixes.** Recording every finding here, and correcting them at Step 26, leaves a clear record of what changed and why.

## What has to happen

- David rates any finding the severity rules do not settle.
- Only David commits the project library, with `commit-all`, after `/mb-close-out`.
