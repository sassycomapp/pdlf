---
title: "f42a-explainer"
doc-id: "mb-7cffd04f"
updated: "2026-11-13"
---
# Step 42A — Release Regression: Explainer

## What it is

Step 42A tests every feature of the release on the test client instance, which is running the new release image.

## How it works

GStack's `/qa-only` runs every feature's flows in Chrome, Firefox and Safari, as each kind of user and signed out. Magnus919's `security-audit-methodology` runs the release's dynamic security scan, planned at Step 15. Any failure moves the test client back to the previous release and stops the release. For App 5's own release, this step is skipped.

## Why it works this way

- **Test what ships.** The release image is what clients will run.

## What has to happen

- David runs the GStack permission command, and moves the test client back if a test fails.
