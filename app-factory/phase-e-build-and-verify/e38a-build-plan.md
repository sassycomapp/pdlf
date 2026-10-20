---
title: "e38a-build-plan"
doc-id: "mb-df4a6f60"
updated: "2026-10-20"
---

## From `pdlf-build-plan.md`: step entry

### Phase E — Build and Verify

Steps 35 to 40B run once per feature, one feature at a time; the run plan governs the loop. Each feature ends with the gate `build-verified` (Step 39).

#### Step 38A: Dependency check

**Must achieve:** Captures Anvil's own security check of the server packages, when the server environment was rebuilt.

**Carried out by:** OpenCode.

**Runs:** once per feature.

**Skills.** None: the step reads Anvil's own check of the server packages and records it → `triage_findings`, then Step 39.
