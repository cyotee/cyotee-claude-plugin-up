# cyotee-claude-plugin-up# cyotee-claude-plugins

Development workflow commands for Claude Code.

## Installation

```bash
# Add this marketplace
/plugin marketplace add cyotee/cyotee-claude-plugins

# Install plugins
/plugin install up@cyotee
/plugin install design@cyotee
/plugin install backlog@cyotee

# Or browse all available
/plugin browse cyotee
```

## Available Plugins

### up

Context bootstrap commands for reading project documentation.

| Command | Description |
|---------|-------------|
| `/up` | Bootstrap with CLAUDE.md |
| `/up:prompt` | Bootstrap with CLAUDE.md + PROMPT.md (for agent worktrees) |
| `/up:plan` | Bootstrap with CLAUDE.md + UNIFIED_PLAN.md (for task overview) |

## Workflow

1. **Start a project:** `/up` to load context
2. **Design features:** `/design <feature-name>` to create tasks
3. **Check status:** `/backlog` to see all tasks
4. **Launch agents:** `/backlog:launch 3` to start work on task 3
5. **Review progress:** `/design:review` to refine tasks

## Related Files

These commands work with:
- `CLAUDE.md` - Project documentation and conventions
- `UNIFIED_PLAN.md` - Task backlog with user stories
- `PROMPT.md` - Agent task instructions (in worktrees)
