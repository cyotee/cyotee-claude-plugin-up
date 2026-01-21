# up - Context Bootstrap Plugin

Bootstrap your AI coding assistant with project context by reading documentation files.

**Dual-Platform Support:** This plugin works with both Claude Code and OpenCode.

## Installation

### Claude Code

```bash
/plugin marketplace add cyotee/cyotee-claude-plugins
/plugin install up@cyotee
```

### OpenCode

Copy or symlink the `.opencode/` directory to your project:

```bash
# Option 1: Symlink (recommended for development)
ln -s /path/to/plugins/up/.opencode/commands ~/.config/opencode/commands/up

# Option 2: Copy to project
cp -r /path/to/plugins/up/.opencode/commands .opencode/commands/
```

Or reference in your `opencode.json`:

```json
{
  "instructions": "{file:.opencode/commands/up.md}"
}
```

## Commands

### `/up`

Load project context by reading CLAUDE.md and any referenced documentation.

**What it does:**
1. Finds CLAUDE.md in the current directory or repository root
2. Reads and internalizes the project instructions
3. Follows references to other CLAUDE.md files (e.g., in submodules)
4. Summarizes what was learned

**Example output:**
```
Context loaded from CLAUDE.md:
- Project: [Project Name] - [Description]
- Architecture: [Key patterns]
- Dependencies: [Key libs/frameworks]
- Also read: [Referenced CLAUDE.md files]

Ready to assist with this codebase.
```

**When to use:** At the start of any Claude Code session to understand the project.

---

### `/up:plan`

Load project context AND the global PRD and task status.

**Aliases:** `/up:prd`

**What it does:**
1. Reads CLAUDE.md and referenced documentation
2. Reads PRD.md for project requirements
3. Scans for tasks/ directories
4. Shows task status summary from INDEX.md
5. Identifies ready and blocked tasks

**Example output:**
```
# Project Context Loaded

## Vision (from PRD.md)
[Project name] - [Vision statement]

## Key Requirements
- [Requirement 1]
- [Requirement 2]

## Task Status (from tasks/INDEX.md)
| # | Title | Status | Layer |
|---|-------|--------|-------|
| [P]-1 | ... | ✅ Complete | [Layer] |
| [P]-2 | ... | 🚀 In Progress | [Layer] |

Ready tasks: [list]
Blocked tasks: [list]
```

**When to use:** When you need to understand both the codebase and current task status.

---

### `/up:prompt`

Load project context AND agent task instructions from PROMPT.md.

**What it does:**
1. Reads CLAUDE.md and referenced documentation
2. Reads PROMPT.md to understand the assigned task
3. Shows task deliverables and inventory checks
4. Prepares to begin work

**Example output:**
```
Context loaded:
- Project: [Project Name]
- Task: [P]-7 - [Task Title]

Assignment:
- [Key deliverable 1]
- [Key deliverable 2]

Inventory checks to perform:
- [ ] [Prerequisite 1]
- [ ] [Prerequisite 2]

Completion promise: TASK_COMPLETE

Beginning work...
```

**When to use:** In agent worktrees after `/backlog:launch` creates the PROMPT.md.

---

## Layer Detection

The `/up:plan` command scans for tasks/ directories:

```bash
find . -type d -name "tasks" -not -path "*/node_modules/*" 2>/dev/null
```

For each discovered tasks/ directory:
1. Read `tasks/INDEX.md` for layer name and task status
2. Display consolidated status across all layers

## Related Files

| File | Purpose |
|------|---------|
| `CLAUDE.md` | Project documentation, conventions, architecture |
| `PRD.md` | Global project requirements |
| `tasks/INDEX.md` | Task backlog with status table |
| `PROMPT.md` | Agent task instructions (in worktrees) |

## Workflow Integration

```
1. /up              # Understand the codebase
2. /up:plan         # See available tasks
3. /backlog:launch  # Create worktree for a task
4. /up:prompt       # (In worktree) Load task instructions
```

## Directory Structure

```
up/
├── .claude-plugin/
│   └── plugin.json          # Claude Code manifest
├── .opencode/
│   └── commands/            # OpenCode-format commands
│       ├── up.md
│       ├── plan.md
│       ├── prd.md
│       └── prompt.md
├── commands/                # Claude Code commands (source of truth)
│   ├── up.md
│   ├── plan.md
│   ├── prd.md
│   └── prompt.md
├── build/
│   ├── translate.ts         # Bun/TypeScript translator
│   └── translate.sh         # Bash translator (fallback)
├── opencode.json            # OpenCode manifest
└── README.md
```

## Building / Syncing

If you modify the Claude Code commands in `commands/`, regenerate the OpenCode versions:

```bash
# Using Bun (recommended)
cd plugins/up
bun run build/translate.ts

# Using Bash (limited agent support)
./build/translate.sh
```

## Platform Differences

| Feature | Claude Code | OpenCode |
|---------|-------------|----------|
| Command prefix | `/up:plan` | `/plan` |
| Tool restrictions | Per-command frontmatter | Per-agent config |
| Model format | `sonnet` | `anthropic/claude-sonnet` |

## License

MIT
