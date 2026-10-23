---
title: "pol-testing-and-quality"
doc-id: "mb-6296454f"
updated: "2026-10-23"
---
# PDLF Policy — Testing and Quality

**Binding.** The agent complies from Step 35 (the build loop) to Step 39 (triage) and the `build-verified` gate. No exceptions without a deviation the developer decides.

How every application is tested is set by the test suite, [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md), and by [[[default:policy-global/pol-testing-and-quality|Policy — Testing and Quality]]](C:/dev/project-library-global/policy-global/pol-testing-and-quality.md): the order of the levels, the local runtime, the two connections, the backups around hosted runs, sign-off and the findings files. This policy holds only what PDLF adds: the order in which the build loop runs its steps.

---

## What

### The per-feature loop

Every feature runs this loop, in this order:

| Step | What it does |
|---|---|
| 35 | Build the feature test-first; Levels 1 and 2 of the test suite. |
| 35A | Broader test coverage and supply-chain checks. |
| 40 | Architecture scan: a read-only report. |
| 40B | Apply the remediation the developer approved at Step 40, if any. |
| 36 | Design check against the approved screens. |
| 37 | Code review and security review. |
| 38 | Functional and regression testing (Level 3), report only. |
| 38A | Pipeline results consolidated. |
| 39 | Triage of the findings of Steps 36 to 38; the `build-verified` gate. |

### Remediation is retested

Remediation from Step 40B is retested by Steps 36 to 38 before the gate. The `build-verified` gate therefore sits at Step 39, after the retest.

### One feature at a time

The next feature enters Step 35 only after the developer has signed off the current one at Step 39.

---

## Why

Remediation that ships without a retest can break what the reviews had just passed. Running Steps 36 to 38 after Step 40B, and placing the gate after them, means nothing reaches the gate unverified. One feature at a time keeps every signed-off feature a known-good baseline, so a later fault can be traced to what came after it.

---

## Where

Steps 35 to 40B and the `build-verified` gate. PDLF's own orchestration is tested with [[[pdlf:pdlf-library/templates-local/chk-pdlf-self-test|PDLF Self-Test Checklist]]](C:/pdlf/pdlf-library/templates-local/chk-pdlf-self-test.md).
