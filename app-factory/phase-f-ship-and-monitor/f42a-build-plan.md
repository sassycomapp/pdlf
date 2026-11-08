---
title: "f42a-build-plan"
doc-id: "mb-f3b31ed1"
updated: "2026-11-08"
---

## From `pdlf-build-plan.md`: step entry

### Phase F — Ship and Monitor

Ends with the gates `production-released` (Step 44) and `released` (Step 46). The release is App 1's approved code pushed into App 2, `master_template`, built with App 3 into the release image, and moved to every client instance by App 5's Release action ([[[default:specifications-global/spec-client-instance-hosting|Client Instance Hosting]]](C:/dev/project-library-global/specifications-global/spec-client-instance-hosting.md)).

#### Step 42A: Release regression test

**Must achieve:** Every feature is tested on the test client instance, running the release image.

**Carried out by:** GStack, using `/qa-only`.

**Skills.** Every skill's output is used by the step named after the arrow.
- `/qa-only` (GStack): tests every feature on the test client instance in a real browser, report only → `f42a` findings, then Step 43; a failure moves the test client instance back to the previous release image.
