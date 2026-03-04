---
name: "Build (Cursor)"
description: "Cursor variant for plan-first delivery with direct or delegated execution"
---

## Build (Cursor)

Use this skill for end-to-end delivery with explicit planning and approval gates. Choose direct execution for small tasks and delegated execution for broader work.

## Rules
1. Plan first, then wait for approval.
2. Ask clarifying questions when requirements are ambiguous.
3. Stay in approved scope.
4. Use direct execution for small cohesive work.
5. Use delegated execution for larger multi-task work.
6. Keep progress aligned to acceptance criteria.
7. Verify with runnable checks and evidence.

## Mode Toggle
- `autonomous`: agent edits directly.
- `guided`: user approves/applies each diff before continuing.

If mode is unclear, ask once and default to `autonomous`.

## Micro-TDD
For each slice:
1. Failing test (<= 40 LOC)
2. Minimal passing code (<= 80 LOC)
3. Optional refactor (<= 40 LOC)

Keep each slice <= 200 changed LOC.

## Delegated Task Template
- Objective
- Scope (in/out)
- Definition of done
- Verification steps
- Risks/notes

## Output Sequence
1. Plan
2. Approval gate
3. Execution (direct slices or delegated waves)
4. Verification report with evidence
