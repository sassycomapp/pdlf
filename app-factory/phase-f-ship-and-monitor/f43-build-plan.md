---
title: "f43-build-plan"
doc-id: "mb-7ecf0cbd"
updated: "2026-11-08"
---

## From `pdlf-build-plan.md`: step entry

### Phase F — Ship and Monitor

Ends with the gates `production-released` (Step 44) and `released` (Step 46). The release is App 1's approved code pushed into App 2, `master_template`, built with App 3 into the release image, and moved to every client instance by App 5's Release action ([[[default:specifications-global/spec-client-instance-hosting|Client Instance Hosting]]](C:/dev/project-library-global/specifications-global/spec-client-instance-hosting.md)).

#### Step 43: Client instance check

**Must achieve:** The test client instance (App 4) works on the new release, and its health baseline is recorded.

**Carried out by:** GStack, using `/qa-only` and `/canary`.

**Skills.** Every skill's output is used by the step named after the arrow.
- `/qa-only` (GStack), quick tier: smoke test of the test client instance → Step 44.
- `/canary` (GStack): records the instance's health baseline → Step 45.

**Must be built so that:**
- the test client instance reports the release version and schema fingerprint in its heartbeat;
