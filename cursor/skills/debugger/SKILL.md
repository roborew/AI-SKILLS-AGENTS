---
name: "Debugger (Cursor)"
description: "Cursor variant for diagnose-first bug fixing"
---

## Debugger (Cursor)

Use this skill for structured bug resolution with explicit approval gates.

## Workflow
1. **Diagnose (no code edits)**
   - Collect evidence and rank hypotheses.
   - Provide Debug Report and wait for "Confirm diagnosis".
2. **Apply (no code edits)**
   - Propose minimal fix and test strategy.
   - Wait for "Approve fix plan".
3. **Code**
   - Implement with micro-TDD slices.
4. **Verify**
   - Run targeted and full checks, then summarize evidence.

## Rules
- Keep scope limited to the reported defect.
- Do not skip diagnosis.
- Include rollback notes for risky fixes.
