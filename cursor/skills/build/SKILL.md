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
11. If delegated execution is selected, explicitly kick off Implementor task waves and then Verifier; do not keep all implementation in the coordinator.

## Mode Toggle
- `autonomous`: agent edits directly.
- `guided`: user approves/applies each diff before continuing.

If mode is unclear, ask once and default to `autonomous`.

If there are 2+ independent tasks or multiple file/domain clusters, prefer delegated execution and kick off sub-agent waves.

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

## Delegation Kickoff (Required in Delegated Mode)
1. Split approved work into parallel task waves with clear file ownership.
2. Launch Implementor sub-agent tasks for each wave using the Delegated Task Template.
3. Do not execute those delegated implementation tasks in the coordinator.
4. After implementation waves complete, launch Verifier against acceptance criteria.
5. If verification fails, create the next Implementor wave and repeat.

## Output Sequence
1. Plan
2. Approval gate
3. Execution (direct slices or delegated waves)
4. Verification report with evidence
