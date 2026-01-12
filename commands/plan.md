---
description: Bootstrap context with CLAUDE.md AND read PRD.md for project requirements
---

# Context Bootstrap with PRD

Read project documentation AND the Product Requirements Document (PRD.md).

## Instructions

1. **Read CLAUDE.md**: Find and read CLAUDE.md in the current working directory or repository root

2. **Follow references**: If CLAUDE.md references other CLAUDE.md files (e.g., in submodules), read those as well

3. **Read design.yaml** (if exists): Understand repo configuration:
   - Repo prefix for task IDs
   - Repo name
   - Submodule configuration

4. **Read PRD.md**: Find and read PRD.md at the repository root to understand:
   - Project vision and goals
   - Target users and use cases
   - High-level requirements
   - Key constraints and non-goals
   - Success metrics

5. **Check task status**: Scan for tasks/ directories:
   ```bash
   find . -type d -name "tasks" -not -path "*/node_modules/*" -not -path "*/archive/*" 2>/dev/null
   ```
   For each discovered tasks/ directory, read its INDEX.md to get layer info and task status.

6. **Summarize**: After reading, provide:
   - Project vision (from PRD.md)
   - Brief technical overview (from CLAUDE.md)
   - Current task status summary (from INDEX.md if exists)
   - Recommended next tasks to work on

## Example Output

```
═══════════════════════════════════════════════════════════════════
 CONTEXT LOADED: Project + Requirements
═══════════════════════════════════════════════════════════════════

## Project Overview

Name: {name}
Purpose: {brief purpose from CLAUDE.md}
Prefix: {PREFIX} (for task IDs)

## Product Requirements (from PRD.md)

Vision: {product vision}
Goals:
- {Goal 1}
- {Goal 2}

Target Users:
- {User type 1}
- {User type 2}

## Task Status (from tasks/INDEX.md)

| ID | Title | Status | Layer |
|----|-------|--------|-------|
| {PREFIX}-001 | ... | Complete | Core |
| {PREFIX}-002 | ... | Ready | Core |
...

Ready for agent: {PREFIX}-002, {PREFIX}-003
Blocked: {PREFIX}-005 (waiting on {PREFIX}-003)

═══════════════════════════════════════════════════════════════════

Ready to assist with this codebase.
```

## If PRD.md doesn't exist

Inform the user:

```
No PRD.md found at repository root.

To create one, run: /design:prd

This will interactively gather project requirements and generate PRD.md.
```

## Related Commands

- `/up` - Just read CLAUDE.md
- `/up:prompt` - Bootstrap for agent worktree (reads PROMPT.md)
- `/backlog` - See detailed task status
- `/design` - Create a new task
