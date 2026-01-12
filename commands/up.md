---
description: Bootstrap context by reading CLAUDE.md and any referenced documentation
argument-hint: [plan|prd|prompt]
---

# Context Bootstrap Command

Read and internalize the project's CLAUDE.md documentation to understand the codebase.

## Instructions

1. **Find CLAUDE.md**: Look for CLAUDE.md in the current working directory or repository root

2. **Read CLAUDE.md**: Read and understand the project instructions, architecture, and conventions

3. **Follow references**: If CLAUDE.md references other CLAUDE.md files (e.g., in submodules like `lib/daosys/lib/crane/CLAUDE.md`), read those as well

4. **Check for design.yaml**: If design.yaml exists, read it to understand:
   - Repo prefix for task IDs
   - Repo name
   - Submodule configuration

5. **Acknowledge**: After reading, briefly confirm what you learned:
   - Project name and purpose
   - Key architectural patterns
   - Important conventions or constraints
   - Any referenced documentation you also read

## Example Output

After reading, respond with something like:

```
═══════════════════════════════════════════════════════════════════
 CONTEXT LOADED
═══════════════════════════════════════════════════════════════════

Project: {name} - {brief purpose}
Repo Prefix: {PREFIX} (for task IDs)

Architecture:
- {Key pattern 1}
- {Key pattern 2}

Dependencies:
- {Key libs/frameworks}

Also read:
- {List of referenced CLAUDE.md files}

Ready to assist with this codebase.

═══════════════════════════════════════════════════════════════════
```

## Related Commands

- `/up:plan` - Also read PRD.md for project requirements
- `/up:prompt` - Bootstrap for agent worktree (reads PROMPT.md)
