# up - Context Bootstrap Plugin

Bootstrap Claude Code with project context by reading documentation files.

## Installation

```bash
/plugin marketplace add cyotee/cyotee-claude-plugins
/plugin install up@cyotee
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
- Project: IndexedEx - Modular DeFi vault infrastructure
- Architecture: Diamond Pattern (EIP-2535), Facet-Target-Repo
- Dependencies: Crane framework, Solady, OpenZeppelin
- Also read: lib/daosys/lib/crane/CLAUDE.md

Ready to assist with this codebase.
```

**When to use:** At the start of any Claude Code session to understand the project.

---

### `/up:plan`

Load project context AND the unified development plan.

**What it does:**
1. Reads CLAUDE.md and referenced documentation
2. Reads UNIFIED_PLAN.md to understand the task backlog
3. Shows task status summary table
4. Identifies ready and blocked tasks

**Example output:**
```
Context loaded:
- Project: IndexedEx - Modular DeFi vault infrastructure
- Architecture: Diamond Pattern (EIP-2535)

Task Status:
| Task | Title                    | Status          |
|------|--------------------------|-----------------|
| 1    | V3 Mainnet Fork Tests    | Complete        |
| 2    | Slipstream Utils         | Complete        |
| 5    | Protocol DETF (CHIR)     | Ready for Agent |

Ready tasks: 5, 6, 7, 8, 9
Blocked tasks: None

Ready to assist with this codebase.
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
- Project: IndexedEx
- Task: 7 - Slipstream Standard Exchange Vault

Assignment:
- Implement single-sided deposits for token0 and token1
- Handle position state transitions
- Auto-compound trading fees

Inventory checks to perform:
- [ ] Slipstream NFT position manager interface available
- [ ] SlipstreamUtils from Task 2 ready

Completion promise: TASK_COMPLETE

Beginning work...
```

**When to use:** In agent worktrees after `/backlog:launch` creates the PROMPT.md.

---

## Related Files

| File | Purpose |
|------|---------|
| `CLAUDE.md` | Project documentation, conventions, architecture |
| `UNIFIED_PLAN.md` | Task backlog with user stories |
| `PROMPT.md` | Agent task instructions (in worktrees) |

## Workflow Integration

```
1. /up              # Understand the codebase
2. /up:plan         # See available tasks
3. /backlog:launch  # Create worktree for a task
4. /up:prompt       # (In worktree) Load task instructions
```

## License

MIT
