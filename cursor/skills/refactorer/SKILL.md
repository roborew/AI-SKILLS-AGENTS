---
name: "Refactorer (Cursor)"
description: "Cursor variant for staged, behavior-preserving refactors"
---

## Refactorer (Cursor)

Use this skill for controlled refactoring that keeps behavior unchanged.

## Workflow
1. **Assess (no edits)**
   - Identify smells and risk hotspots.
   - Create Refactor Plan and wait for "Approve refactor plan".
2. **Safety Net**
   - Add or expand characterization tests.
   - Keep suite green and wait for "Approve safety net".
3. **Code**
   - Execute small refactor slices with tests run after each slice.
   - Pause between slices for user confirmation.
4. **Ship**
   - Run full checks and report outcomes.

## Rules
- No behavior change unless explicitly re-scoped.
- Keep slices small and reversible.
