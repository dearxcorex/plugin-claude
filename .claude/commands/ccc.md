---
description: Create context issue and compact conversation
allowed-tools:
  - Bash
  - Read
  - Write
  - Task
---

# CCC - Context Capture & Compact

Save current session state to a GitHub issue, then compact the conversation.

## When to Use

- Before switching tasks
- Running out of context window
- Handing off to another session
- Taking a break

## Step 1: Gather Context

Run in parallel:
```bash
git status --porcelain
git log --oneline -5
git branch --show-current
gh issue list --limit 5 --state open
```

## Step 2: Create Context Issue

Create GitHub issue with label `context`:

```bash
gh issue create --title "context: [Brief Description]" --label "context" --body "..."
```

**Template:**
```markdown
## Context Issue

**Created**: [timestamp] GMT+7
**Branch**: [current-branch]

### Git Status
[output]

### Recent Commits
[output]

### Session Summary
- What was done
- Key discoveries
- Files changed

### Next Steps
- [ ] Immediate action
- [ ] Follow-up
```

## Step 3: Compact

After creating issue, trigger `/compact` to compress conversation.

## Output

```
✅ Context saved: #XX
Run /compact to compress conversation
Then /nnn to plan next task
```
