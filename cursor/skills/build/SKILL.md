---
name: "Build (Cursor)"
description: "Cursor variant for plan-first delivery with direct or delegated execution"
---

## Build (Cursor)

Use this skill for end-to-end delivery with explicit planning and approval gates. Choose direct execution for small tasks and delegated execution for broader work.

## Guiding Principles
- **Framework alignment**: infer stack conventions from the repo (or ask once) and implement idiomatically.
- **Engineering foundations**: apply DRY, SOLID, and clear domain boundaries as appropriate.
- **Micro-TDD discipline**: deliver in small red/green/refactor slices with explicit verification.
- **Performance awareness**: watch hot paths, Big-O implications, and DB/query pressure; propose indexing/caching where needed.
- **Clean quality gates**: keep tests and linters green through each slice.
- **Mentor compatibility**: if mentor mode is active or user asks to explain more, keep the same workflow but add layered explanations.

## Rules
1. Plan first, then wait for approval.
2. Ask clarifying questions when requirements are ambiguous.
3. Stay in approved scope.
4. Use direct execution for small cohesive work.
5. Use delegated execution for larger multi-task work.
6. Keep progress aligned to acceptance criteria.
7. Verify with runnable checks and evidence.
8. In autonomous mode, do not start code changes until implementation plan is approved.
9. TDD is mandatory for behavior changes: write a failing test before production code.
10. If a failing test cannot be written first, stop and report blocker; do not proceed with behavior code.

## Mode Toggle
- `autonomous`: agent edits directly.
- `guided`: user approves/applies each diff before continuing.

If mode is unclear, ask once and default to `autonomous`.

## Micro-TDD
For each behavior slice (required order, no skipping):
1. Add one failing test first (target <= 40 LOC).
2. Run the targeted test and confirm failure (red).
3. Add minimal passing code (target <= 80 LOC).
4. Re-run the targeted test and confirm pass (green).
5. Optional cleanup/refactor (target <= 40 LOC), then re-run tests.

Keep each slice <= 200 changed LOC.

## TDD Enforcement Gate
- If behavior code changes but no new/updated test exists, return `TEST_GATE_FAILED`.
- For each slice, report evidence: test file path, red command/result, green command/result.

## Quality Checks Per Slice
- Re-run targeted tests for the changed behavior.
- Keep lint/style checks clean for touched code.
- Note any performance or DB-query impact introduced by the slice.

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
