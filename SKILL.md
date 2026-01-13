---
name: up
description: Context bootstrap skill equivalent to the cyotee `/up` Claude plugin.
metadata:
  short-description: Load CLAUDE/PRD/task context and summarize for Codex sessions.
---

# up (Codex)

Use this skill at the start of a session or when entering a worktree to load project/task context.

## Modes
- `up`: Read `CLAUDE.md` and any referenced docs (including submodules). Summarize project purpose, architecture, conventions, and important constraints.
- `up:plan` (`up:prd` alias): Read `CLAUDE.md` + `PRD.md`; scan for `tasks/` directories; summarize task status from `tasks/INDEX.md` (ready vs blocked).
- `up:prompt`: In a worktree, read `CLAUDE.md` + `PROMPT.md` to capture the assigned task, deliverables, inventory checks, and completion promise (e.g., `TASK_COMPLETE`). Include quick instructions for how to proceed.

## How to Use
1) Locate the repo root (`git rev-parse --show-toplevel`). Prefer root-level `CLAUDE.md`; if not found, search downward for the nearest one and follow its links.  
2) For `plan`/`prd`:  
   - Load `PRD.md` (if present) and extract vision/goals/constraints.  
   - Find `tasks/` directories (avoid node_modules). For each, read `tasks/INDEX.md` if present; otherwise derive task statuses from directory names.  
   - List ready vs blocked tasks and note dependencies.  
3) For `prompt`:  
   - Read `PROMPT.md` in the worktree root.  
   - Identify task ID/title, deliverables, inventory checks, and completion promise.  
   - Remind the user to keep `PROGRESS.md` updated and to re-run `up:prompt` after `/compact`.
4) Return a concise summary plus any missing-file warnings.

## Conventions
- Respect icons/status values from `tasks/INDEX.md` (🆕 pending, 🚀 in_progress, 📋 review, ✅ complete).
- When multiple CLAUDE.md files exist, follow explicit references before guessing related docs.
- Do not overwrite files; this skill is read-only unless the user asks for edits.
