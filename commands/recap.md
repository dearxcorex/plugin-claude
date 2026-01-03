---
description: Fresh start summary for new sessions
allowed-tools:
  - Bash
  - Read
  - Task
---

# RECAP - Fresh Start Summary

Get up to speed quickly when starting a new session.

## Step 1: Gather Context (Parallel)

```bash
gh issue list --label "context" --limit 3 --state all
gh issue list --search "plan:" --limit 3 --state all
git log --oneline -10
git status --short
gh pr list --state open
ls -la .ccc/memory/retrospectives/ 2>/dev/null | tail -5
```

## Step 2: Read Key Files

If they exist:
- `.ccc/HOME.md`
- `.ccc/WIP.md`
- Most recent retrospective
- Most recent context issue

Use `context-finder` agent:
```
Task: subagent_type=context-finder, model=haiku
Find recent context: retrospectives, WIP, context issues
```

## Step 3: Generate Summary

```markdown
## Session Recap

**Project**: [name]
**Last Active**: [from context/retro]
**Branch**: [current]

### Where We Left Off
[from most recent context issue or retrospective]

### Recent Activity
- [commit 1]
- [commit 2]

### Open Items
| Type | # | Title | Status |
|------|---|-------|--------|
| Plan | 5 | [title] | Ready |
| PR | 2 | [title] | Review |
| Issue | 3 | [title] | Open |

### Current WIP
[from WIP.md]

### Suggested Next Steps
1. [based on open plan]
2. [based on WIP]
3. [based on PRs]

### Quick Commands
- `/lll` - Full status
- `/nnn` - Plan next task
- `/gogogo` - Execute pending plan
```

## Output

Concise summary to start working immediately.
