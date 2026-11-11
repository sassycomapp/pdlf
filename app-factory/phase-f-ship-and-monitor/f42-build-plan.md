---
title: "f42-build-plan"
doc-id: "mb-204ff45b"
updated: "2026-11-11"
---

## From `pdlf-build-plan.md`: step entry

### Phase F — Ship and Monitor

Ends with the gates `production-released` (Step 44) and `released` (Step 46). The release is App 1's approved code pushed into App 2, `master_template`, built with App 3 into the release image, and moved to every client instance by App 5's Release action ([[[default:specifications-global/spec-client-instance-hosting|Client Instance Hosting]]](C:/dev/project-library-global/specifications-global/spec-client-instance-hosting.md)).

#### Step 42: Release to App 2

**Must achieve:** App 1's tagged release is pushed into App 2, `master_template`, its table changes are written into App 3's table definitions, the release image is built, scanned, signed and checked, and the test client instance runs it by its digest.

**Carried out by:** The developer, after approving the release.

**Skills.** Every skill's output is used by the step named after the arrow.
- `wizard` (Matt Pocock): the developer's instructions to push App 1's tagged release into App 2's repository, to write the release's table changes into App 3's table definitions, and to roll back as below → Step 42A.

**Testing:** App 2's code matches App 1's tag exactly; the release image under the release tag holds App 2, App 3 and `m3` at that release (test RL-04); the table-change check passes (test RL-03).

**Standards:** [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md), [[[default:specifications-global/spec-deployment|Deployment]]](C:/dev/project-library-global/specifications-global/spec-deployment.md), [[[default:specifications-global/spec-client-instance-hosting|Client Instance Hosting]]](C:/dev/project-library-global/specifications-global/spec-client-instance-hosting.md).

**Must be built so that:**
- before the push, every client instance copies its data to its own R2 bucket;
- the image build workflow in `{slug}-app4` builds the release image from the release tag and stores it under that tag; the build stops if App 3 holds any form or server module, or if the table-change check finds a table or column removed, renamed or retyped;
- the image build workflow scans the release image and signs it; the build fails if the image contains end-of-life software, and the release stops while any high or critical finding is older than 14 days;
- the whole test suite passes on the release image;
- App 5 verifies the image's signature and moves the test client instance to the release image by its digest, and its App Server adds the release's new tables and columns;
- rollback moves client instances back to the previous release image with `auto-migrate` off, as the deployment specification sets out;
