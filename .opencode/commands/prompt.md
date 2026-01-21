---
description: Bootstrap context for agent execution - read CLAUDE.md AND PROMPT.md task instructions
---

# Agent Task Bootstrap

Read project documentation AND the current PROMPT.md task instructions. Use this when starting work in an agent worktree.

This command is **mode-aware** - it adapts based on whether PROMPT.md is set to Implementation or Code Review mode.

## Instructions

1. **Read CLAUDE.md**: Find and read CLAUDE.md in the current working directory or repository root

2. **Follow references**: If CLAUDE.md references other CLAUDE.md files (e.g., in submodules), read those as well

3. **Read PROMPT.md**: Find and read PROMPT.md in the current directory to understand:
   - The task ID and title
   - The **mode** (Implementation or Code Review)
   - The task directory path
   - Required files to read

4. **Read referenced task files** (as specified in PROMPT.md):
   - `tasks/{ID}-{name}/TASK.md` - Requirements
   - `tasks/{ID}-{name}/PROGRESS.md` - Prior work
   - `tasks/{ID}-{name}/REVIEW.md` - Review document (for review mode)

5. **Mode-specific bootstrap:**

### Implementation Mode

If PROMPT.md contains `**Mode:** Implementation`:

```
═══════════════════════════════════════════════════════════════════
 AGENT BOOTSTRAPPED - Implementation
═══════════════════════════════════════════════════════════════════

Project: {name from CLAUDE.md}
Task: {PREFIX}-{NNN} - {Title}
Mode: Implementation

## Requirements (from TASK.md)

- {User story 1}
- {User story 2}
- ...

## Prior Progress (from PROGRESS.md)

Last checkpoint: {summary}
Next step: {what to do next}

## Continuing From

{Specific place to resume work}

## Completion

When done: <promise>TASK_COMPLETE</promise>
If blocked: <promise>TASK_BLOCKED: [reason]</promise>

═══════════════════════════════════════════════════════════════════

Beginning work...
```

### Code Review Mode

If PROMPT.md contains `**Mode:** Code Review`:

```
═══════════════════════════════════════════════════════════════════
 AGENT BOOTSTRAPPED - Code Review
═══════════════════════════════════════════════════════════════════

Project: {name from CLAUDE.md}
Reviewing: {PREFIX}-{NNN} - {Title}
Mode: Code Review

## Implementation Summary (from PROGRESS.md)

- {What was completed}
- Tests: {status}
- Build: {status}

## Requirements to Verify (from TASK.md)

- [ ] {Acceptance criterion 1}
- [ ] {Acceptance criterion 2}
- ...

## Review Focus

- Verify all acceptance criteria are met
- Check test coverage
- Look for bugs, edge cases, security issues
- Document findings in REVIEW.md

## Prior Review Progress (from REVIEW.md)

{Summary of prior findings, or "Starting fresh review"}

## Completion

When review done: <promise>REVIEW_COMPLETE</promise>

═══════════════════════════════════════════════════════════════════

Beginning review...
```

## Expected PROMPT.md Structure

PROMPT.md files contain:
- Task ID and title
- Mode (Implementation or Code Review)
- Task directory path
- Required reading list
- Mode-specific instructions
- Completion promise format

## On Context Compaction

If your context is compacted or you're resuming work:
1. Re-run `/prompt`
2. This will re-read PROMPT.md and task files
3. Continue from where PROGRESS.md (or REVIEW.md) indicates

## Error Handling

- **No PROMPT.md**: "No PROMPT.md found. Are you in an agent worktree? Use /launch to create one."
- **No TASK.md**: "Task file not found at path specified in PROMPT.md"
- **Invalid mode**: Default to Implementation mode

## Related Commands

- `/up` - Just read CLAUDE.md
- `/plan` - Read CLAUDE.md + PRD.md
