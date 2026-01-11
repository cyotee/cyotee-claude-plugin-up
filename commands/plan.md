---
description: Bootstrap context with CLAUDE.md AND read PRD.md for project requirements
---

# Context Bootstrap with Project Requirements

Read project documentation AND the global Product Requirements Document (PRD.md).

## Instructions

1. **Read CLAUDE.md**: Find and read CLAUDE.md in the current working directory or repository root

2. **Follow references**: If CLAUDE.md references other CLAUDE.md files (e.g., in submodules), read those as well

3. **Read PRD.md**: Find and read PRD.md at the repository root to understand:
   - Project vision and goals
   - High-level requirements
   - Key constraints and non-goals
   - Target users and use cases
   - Success metrics

4. **Check task status**: Scan for tasks/ directories:
   ```bash
   find . -type d -name "tasks" -not -path "*/node_modules/*" -not -path "*/archive/*" 2>/dev/null
   ```
   For each discovered tasks/ directory, read its INDEX.md to get layer info and task status.

5. **Summarize**: After reading, provide:
   - Project vision (from PRD.md)
   - Brief technical overview (from CLAUDE.md)
   - Current task status summary (from INDEX.md if exists)
   - Recommended next tasks to work on

## Example Output

```
# Project Context Loaded

## Vision (from PRD.md)
[Project name] - [1-2 sentence vision statement]

## Key Requirements
- [Requirement 1]
- [Requirement 2]
- [Requirement 3]

## Technical Overview (from CLAUDE.md)
- Architecture: [key patterns]
- Dependencies: [key libs/frameworks]

## Task Status (from tasks/INDEX.md)
| # | Title | Status | Layer |
|---|-------|--------|-------|
| [P]-1 | ... | ✅ Complete | [Layer] |
| [P]-2 | ... | 🚀 In Progress | [Layer] |

Ready tasks: [list tasks ready for agent]
Blocked tasks: [list blocked tasks and why]

Ready to assist with this codebase.
```

## If PRD.md doesn't exist

Inform the user:

```
No PRD.md found at repository root.

To create one, run: /design:prd

This will interactively gather project requirements and generate PRD.md.
```
