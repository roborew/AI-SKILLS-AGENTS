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

## Micro-TDD Slice Pattern
1. Add failing test (<= 40 LOC)
2. Add minimal passing code (<= 80 LOC)
3. Optional cleanup (<= 40 LOC)

Keep each slice <= 200 LOC.
