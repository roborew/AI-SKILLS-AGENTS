# AI Skills and Agent Setup

This repository is organized into two parallel platforms with matching naming and structure:

- `opencode/skills/` + `opencode/agents/`
- `cursor/skills/` + `cursor/agents/`

Both platforms now use the same 9 agent names:
`plan`, `build`, `implementor`, `verifier`, `debugger`, `refactorer`, `pr-reviewer`, `ui-designer`, `mentor`.

## What Changed

The previous 12-skill layout had overlap. It is consolidated to 9:

- `plan` merges Investigator + Architect + UX Reviewer
- `build` merges Developer + Coordinator
- 7 specialist skills remain focused and unchanged in intent:
  `implementor`, `verifier`, `debugger`, `refactorer`, `pr-reviewer`, `ui-designer`, `mentor` (renamed from mentor-mode)

This keeps all valuable guidance while removing repeated instructions.

## Skills vs Agents

- A **skill** is the full behavior prompt (`skills/<name>/SKILL.md`).
- An **agent** is the runtime configuration (`agents/<name>.md`) that loads a skill prompt and defines mode/tool access.

In practice: agent config files are what you copy into your runtime agent directory, and they reference the corresponding skill prompt.

## OpenCode Strategy

### Primary agents

| Agent | Mode | Purpose |
| --- | --- | --- |
| `plan` | primary (read-only) | Solution, architecture, and UX analysis before code |
| `build` | primary (full tools) | Delivery agent: direct implementation for small tasks, delegation for larger tasks |

### Subagents

| Agent | Role |
| --- | --- |
| `implementor` | Leaf executor for scoped implementation tasks |
| `verifier` | Evidence-based acceptance verification |
| `debugger` | Diagnose-first bug orchestrator |
| `refactorer` | Behavior-preserving refactor orchestrator |
| `pr-reviewer` | Merge-readiness gatekeeper (review + tests + coverage) |
| `ui-designer` | UI specialist with accessibility constraints |
| `mentor` | Teaching overlay that preserves active workflow constraints |

## Delegation Mechanics (Task Tool)

When a skill says "delegate to Implementor" or "delegate to Verifier", this means:

1. The current agent invokes the **Task** tool.
2. The Task call targets a configured subagent (for example `implementor`).
3. The subagent executes scoped work and reports results back.

Built-in OpenCode subagents (`general`, `explore`) are still useful utility agents. Your custom subagents add stronger, workflow-specific behavior (micro-TDD, strict gate checks, review criteria, etc.).

## End-to-End Workflow

1. **Understand**: `plan`
2. **Implement**: `build` (directly or via `implementor`)
3. **Verify**: `verifier`
4. **Review/Merge gate**: `pr-reviewer`

Utility paths:

- Bugs: `debugger -> implementor -> verifier`
- Refactors: `refactorer -> implementor -> verifier`
- UI-heavy work: `ui-designer` (optionally with `verifier`)
- Learning mode: `mentor` overlay on any stage

## Folder Layout

```text
opencode/
  skills/
    plan/SKILL.md
    build/SKILL.md
    implementor/SKILL.md
    verifier/SKILL.md
    debugger/SKILL.md
    refactorer/SKILL.md
    pr-reviewer/SKILL.md
    ui-designer/SKILL.md
    mentor/SKILL.md
  agents/
    plan.md
    build.md
    implementor.md
    verifier.md
    debugger.md
    refactorer.md
    pr-reviewer.md
    ui-designer.md
    mentor.md

cursor/
  skills/
    plan/SKILL.md
    build/SKILL.md
    implementor/SKILL.md
    verifier/SKILL.md
    debugger/SKILL.md
    refactorer/SKILL.md
    pr-reviewer/SKILL.md
    ui-designer/SKILL.md
    mentor/SKILL.md
  agents/
    plan.md
    build.md
    implementor.md
    verifier.md
    debugger.md
    refactorer.md
    pr-reviewer.md
    ui-designer.md
    mentor.md
```

## Cursor Section

Cursor mirrors the same agent names and layout for consistency. Prompt content is Cursor-flavored, but workflow intent is aligned with OpenCode:

- `plan` for read-only analysis
- `build` for plan-first delivery
- specialist skills for implementation, verification, debugging, refactoring, PR gating, UI, and mentoring
