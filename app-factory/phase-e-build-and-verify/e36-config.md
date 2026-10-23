---
title: "e36-config"
doc-id: "mb-67e8bd49"
updated: "2026-10-23"
---

## From `step-mapping.md`: this step's rows

### Phase D — Build & Verify (per-feature loop)

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 36 | `[[step-36-design-review]]` | Skill | GStack `/design-review` — retest, post-remediation | |

### Phase D — Build & Verify (per-feature loop): phase notes

Repeats once per feature/package from Step 19's ticket list, until every feature has
individually reached `build-verified`. For the loop's actual order and dependencies, see
Run Plan, "Step 35 Feature Loop."


Exit gate: `build-verified`, evaluated per feature. For entry condition and dependencies,
see Run Plan.

## From `bft-checkpoint-cheatsheet-v2.md`: BFT level

### Phase E — Build & Verify (Steps 35–40)

| Step | Name | Type | BFT | Rationale |
|---|---|---|---|---|
| 36 | /design-review | Skill | **Full** | Live-site visual audit, post-remediation retest — design quality decisions |
