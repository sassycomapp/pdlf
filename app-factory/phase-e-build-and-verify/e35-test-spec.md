---
title: "e35-test-spec"
doc-id: "mb-e4dc7f9d"
updated: "2026-11-13"
---
# Step 35: Build — Test Specification

**Proves:** The feature is built test-first, its forms match their approved screen requirements, it is proven at Levels 0 to 3, and David signs it off.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\e35\`; every result is recorded in `{slug}-e35-{run}-{ticket}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | The entry record is complete and Step 34, or the previous ticket's Step 39, is complete. |
| LG-01 | Each behaviour test-first. |
| LG-02 | Edges, odd and hostile input. |
| LG-03 | Lifecycle transitions. |
| LG-04 | Money exact. |
| LG-05 | Time right. |
| LG-06 | Real code tested. |
| IN-01 | The app runs locally. |
| IN-02 | Every new function for every role. |
| IN-03 | Own records only. |
| IN-04 | Allowed fields only. |
| IN-07 | New webhooks verified and exactly-once. |
| IN-11 | New tasks correct. |
| SC-05 | Form checks enforced by the server. |
| SC-06 | Hostile input harmless. |
| ST-11 | The ticket's forms obey the UI rules. |
| DC-13 | Each form holds exactly the components its approved screen requirement names; its spec sheet matches; only handler bodies were changed by Anvil's agent. |
| DM-01 to DM-10 | Each domain rule the ticket touches. |
| BR-01 | Flows end to end, desktop and phone. |
| BR-02 | Edge cases and errors. |
| IN-18 | Hosted test data removed. |
| BR-09 | David signs the feature off. |
| PR-07 | No test weakened. |
| PR-04 | Sentinel ran at High. |

**On failure:** A failing test stops the build: root cause found, code fixed, level run again.
