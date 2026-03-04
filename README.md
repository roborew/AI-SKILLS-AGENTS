# Using These Skills and Subagents

This README is a usage guide for the skill + agent packs in this repository.

## Core Idea

- A **skill** is the prompt content in `skills/<name>/SKILL.md`.
- An **agent** is the runnable config in `agents/<name>.md` that loads a skill prompt.

Use the agent files to run workflows. Skill files are the behavior definitions behind them.

For OpenCode, use built-in primary agents (`plan`, `build`) and custom subagents from this repo.

## Agent Set

OpenCode (recommended):
- Primary (built-in): `plan`, `build`
- Custom subagents from this repo: `implementor`, `verifier`, `debugger`, `refactorer`, `pr-reviewer`, `ui-designer`, `mentor`

Cursor:
- Use the included agent pack in `cursor/agents/` and matching prompts in `cursor/skills/`

## Setup

### OpenCode setup (default)

1. Keep OpenCode built-in primaries: `plan`, `build`.
2. Copy only subagent files from `opencode/agents/` into your OpenCode agents directory.
3. Keep `opencode/skills/` available so `prompt: "{file:...}"` references resolve.
4. If you want custom behavior in built-in primaries, set the built-in `plan`/`build` prompt fields to use:
   - `opencode/skills/plan/SKILL.md`
   - `opencode/skills/build/SKILL.md`
5. Restart/reload OpenCode.

### OpenCode config patch (recommended)

Use this in your existing `opencode.json` to keep built-in primaries (`plan`, `build`) while loading your custom skill prompts:

```json
{
  "agent": {
    "plan": {
      "prompt": "{file:./opencode/skills/plan/SKILL.md}"
    },
    "build": {
      "prompt": "{file:./opencode/skills/build/SKILL.md}"
    },
    "implementor": {
      "description": "Scoped leaf executor for implementation tasks",
      "mode": "subagent",
      "prompt": "{file:./opencode/skills/implementor/SKILL.md}"
    },
    "verifier": {
      "description": "Evidence-driven acceptance verifier",
      "mode": "subagent",
      "prompt": "{file:./opencode/skills/verifier/SKILL.md}"
    },
    "debugger": {
      "description": "Diagnose-first bug orchestrator",
      "mode": "subagent",
      "prompt": "{file:./opencode/skills/debugger/SKILL.md}"
    },
    "refactorer": {
      "description": "Behavior-preserving refactor orchestrator",
      "mode": "subagent",
      "prompt": "{file:./opencode/skills/refactorer/SKILL.md}"
    },
    "pr-reviewer": {
      "description": "Merge-readiness gatekeeper",
      "mode": "subagent",
      "prompt": "{file:./opencode/skills/pr-reviewer/SKILL.md}"
    },
    "ui-designer": {
      "description": "UI specialist",
      "mode": "subagent",
      "prompt": "{file:./opencode/skills/ui-designer/SKILL.md}"
    },
    "mentor": {
      "description": "Teaching overlay",
      "mode": "subagent",
      "prompt": "{file:./opencode/skills/mentor/SKILL.md}"
    }
  }
}
```

You can still use `"/skill"` ad hoc, but config-level prompts keep `plan` and `build` behavior consistent every session.

### Cursor setup

1. Copy `cursor/agents/*.md` into your Cursor agent directory.
2. Keep `cursor/skills/` alongside agent configs.
3. Restart/reload Cursor agent runtime if needed.

## When to Use Each Agent

| Agent | Use it for | Typical output |
| --- | --- | --- |
| `plan` | read-only analysis of solution + architecture + UX (built-in primary in OpenCode) | options, trade-offs, recommendation |
| `build` | primary delivery flow (built-in primary in OpenCode) | implementation plan, code changes, delegated tasks |
| `implementor` | focused scoped coding task | minimal diff + verification notes |
| `verifier` | acceptance criteria checks | evidence-backed verdict |
| `debugger` | diagnose-first bug flow | root cause, fix plan, validated fix |
| `refactorer` | behavior-preserving cleanup | phased refactor with safety checks |
| `pr-reviewer` | merge gate | review findings, tests/coverage/mergeability status |
| `ui-designer` | UI implementation | design-system-consistent, accessible UI changes |
| `mentor` | teaching overlay | layered explanations without changing workflow constraints |

## Delegation and Automation

### What you call manually

- Start analysis with `plan`.
- Start delivery with `build`.
- Run final gate with `pr-reviewer`.
- Invoke `mentor` when you want teaching mode.

### What should be automated

Inside delivery flows, let agents delegate with Task tool:

- `build -> implementor` for scoped implementation
- `build -> verifier` for acceptance checks
- `debugger -> implementor -> verifier`
- `refactorer -> implementor -> verifier`
- `pr-reviewer -> implementor` for fixes and `-> verifier` for re-checks

## Standard Workflow (Feature)

1. **Analyze**
   - Call `plan` to evaluate options and pick a direction.
2. **Implement**
   - Call `build` with approved scope and acceptance criteria.
3. **Verify**
   - Call `verifier` for evidence-driven acceptance validation.
4. **Review**
   - Call `pr-reviewer` for final merge readiness (review + tests + coverage).

## Standard Workflow (UI Feature)

1. `plan` for UX + implementation options.
2. `build` to execute the approved approach.
3. `ui-designer` for UI-heavy slices (usually delegated by `build`).
4. `verifier` to validate acceptance criteria and accessibility outcomes.
5. `pr-reviewer` to confirm merge readiness.

## Copy/Paste Prompts

### Kickoff in `plan`

`Analyze this feature request and provide solution options, architecture implications, UX risks, and a recommendation. Do not edit code.`

### Handoff to `build`

`Implement the approved approach using the acceptance criteria below. Delegate where useful and keep scope tight.`

### Verification

`Verify this implementation strictly against acceptance criteria. Provide evidence and verdict.`

### Merge gate

`Review this change for merge readiness. Report high-confidence issues, test status, coverage status, and remaining blockers.`

## Folder Layout

```text
opencode/
  skills/
  agents/

cursor/
  skills/
  agents/
```

OpenCode note: `opencode/agents/` includes subagents only. Use built-in OpenCode `plan` and `build` as primaries.
