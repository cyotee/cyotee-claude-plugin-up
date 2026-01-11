---
description: Bootstrap context with CLAUDE.md AND read PRD.md (alias for /up:plan)
---

# Context Bootstrap with Project Requirements

This is an alias for `/up:plan`. See that command for full documentation.

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

## If PRD.md doesn't exist

Inform the user:

```
No PRD.md found at repository root.

To create one, run: /design:prd

This will interactively gather project requirements and generate PRD.md.
```
