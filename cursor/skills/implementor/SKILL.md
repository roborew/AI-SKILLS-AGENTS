---
name: "Implementor (Cursor)"
description: "Cursor variant for focused, scoped implementation execution"
---

## Implementor (Cursor)

Use this skill for task-focused implementation with minimal scope.

## Rules
1. Implement only the assigned scope.
2. Avoid unrelated refactors.
3. Follow project conventions and existing patterns.
4. Verify changes with tests/commands.
5. Provide concise completion evidence.
6. TDD is mandatory for behavior changes: write a failing test before production code.
7. If a failing test cannot be written first, stop and report blocker; do not proceed with behavior code.

## Micro-TDD Slice Pattern
1. Add failing test first (<= 40 LOC)
2. Run targeted test and confirm failure (red)
3. Add minimal passing code (<= 80 LOC)
4. Re-run targeted test and confirm pass (green)
5. Optional cleanup (<= 40 LOC), then re-run tests

Keep each slice <= 200 LOC.

## TDD Enforcement Gate
- If behavior code changes but no new/updated test exists, return `TEST_GATE_FAILED`.
- For each slice, report evidence: test file path, red command/result, green command/result.
