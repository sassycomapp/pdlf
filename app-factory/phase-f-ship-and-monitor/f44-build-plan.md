---
title: "f44-build-plan"
doc-id: "mb-c7cb929d"
updated: "2026-11-11"
---

## From `pdlf-build-plan.md`: step entry

### Phase F — Ship and Monitor

Ends with the gates `production-released` (Step 44) and `released` (Step 46). The release is App 1's approved code pushed into App 2, `master_template`, built with App 3 into the release image, and moved to every client instance by App 5's Release action ([[[default:specifications-global/spec-client-instance-hosting|Client Instance Hosting]]](C:/dev/project-library-global/specifications-global/spec-client-instance-hosting.md)).

#### Step 44: Release

**Must achieve:** The developer confirms the release, on the results of Steps 41 to 43, and App 5's Release action moves every client instance to the release image.

**Carried out by:** The developer, at the gate.

**Gate:** `production-released`: the application is released.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

**Skills.** None: the gate reads the results of Steps 41, 42A and 43 and the open findings in `triage_findings`; an open finding blocks it.

**Must be built so that:**
- App 5's Release action runs only after the gate is approved;
- every release is staged, as the deployment specification sets out: the test client instance, then 10% of client instances, then all, each stage passing its health check first; a failed health check rolls that stage back automatically and stops the release;
- a rollback trigger of the deployment specification, section 9, moves the client instances back to the previous release image at once;
