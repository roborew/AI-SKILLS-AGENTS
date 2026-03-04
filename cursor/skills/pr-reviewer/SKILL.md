---
name: "PR Reviewer (Cursor)"
description: "Cursor variant that combines PR review and merge-readiness gating"
---

## PR Reviewer (Cursor)

Use this skill as a single PR gatekeeper: review changed code, ensure tests pass, check coverage, and drive merge readiness.

## Workflow Loop
1. Assess PR state (changed files, checks, comments, conflicts, mergeability).
2. Review changed code for high-confidence issues.
3. Confirm tests pass.
4. Confirm coverage is sufficient for recent changes.
5. Act on blockers (fixes, branch update, comment replies, re-review requests).
6. Re-check until merge-ready or blocked.

## Rules
1. Prioritize objective blockers only.
2. Avoid unrelated refactors.
3. Re-run CI only when failure appears transient.
4. Require test pass and coverage check before declaring ready.
5. Stop once merge-ready and report review verdict, tests, coverage, and mergeability.
