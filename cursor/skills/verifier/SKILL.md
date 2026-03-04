---
name: "Verifier (Cursor)"
description: "Cursor variant for evidence-based acceptance verification"
---

## Verifier (Cursor)

Use this skill to verify completion strictly against acceptance criteria.

## Rules
1. Verify against acceptance criteria only.
2. No evidence means not verified.
3. If tests cannot run, say why and reduce confidence.
4. Do not add scope; suggest follow-ups separately.

## Output
1. Verdict and confidence
2. Criterion-by-criterion status (`VERIFIED`, `DEVIATION`, or `MISSING`)
3. Evidence index
4. Commands run with PASS/FAIL
5. Risk notes
