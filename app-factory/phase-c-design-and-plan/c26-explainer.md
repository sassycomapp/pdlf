---
title: "c26-explainer"
doc-id: "mb-f48ddbe5"
updated: "2026-11-12"
---
# Step 26 — Screens Approved: Explainer

## What it is

Step 26 corrects the screen requirements with the findings of Step 23, has David approve every screen requirement, and asks him to lock them at the gate `screens-approved`. It closes Phase C.

## How it works

The agent corrects every high finding, including every place where a plainer component was chosen over a better one in `m3-custom-theme`; those findings cannot be declined. For medium and low findings, David decides: correct it, or decline it with a reason. Each corrected requirement is checked again.

David then approves each screen requirement on its own, and the agent marks it approved. When every finding is closed and every screen is approved, the agent shows David the gate summary and asks whether to proceed to Phase D. On his yes, David records the gate with `pdlf-gate.sh`.

From here, each form is built by `mb-form-builder`, feature by feature, after the feature's server code exists, exactly as its approved screen requirement says.

## Why it works this way

- **Approved before built.** The builder works only from approved screens, so the design David sees is the design that gets built.
- **Full use of the theme, enforced.** A better-fitting theme component always replaces a plainer one; no screen reaches the builder with a weaker choice.
- **One screen at a time.** David approves each requirement on its own, so nothing is approved without being seen.

## What has to happen

- David decides each medium and low finding.
- David approves each screen requirement.
- David answers the gate: yes to proceed to Phase D, or no to stop. On yes, he runs the `pdlf-gate.sh` command the agent gives him.
- Only David commits the project library, with `commit-all`, after `/mb-close-out`.
