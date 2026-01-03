---
description: Forward context before /clear
allowed-tools:
  - Bash
  - Read
  - Write
---

# FORWARD - Forward Context

Capture and forward context before clearing conversation.

## When to Use

- Before `/clear`
- Context window getting full
- Quick handoff (lighter than full `/ccc` + `/rrr`)

## Step 1: Capture State

```bash
git status --short
git log --oneline -5
git branch --show-current
git diff --stat
```

## Step 2: Create Forward Note

Create lightweight context issue:

```bash
gh issue create --title "forward: [Brief]" --label "forward" --body "..."
```

**Template:**
```markdown
## Forward Context

**Created**: [timestamp] GMT+7
**Type**: Forward (pre-clear)
**Branch**: [branch]

### Session Topics
- [topic 1]
- [topic 2]

### Key Decisions
- [decision]: [rationale]

### Code Changes
- [file]: [what changed]

### Unfinished
- [ ] [incomplete 1]
- [ ] [incomplete 2]

### Resume With
1. Checkout: `git checkout [branch]`
2. Run: `/recap`
3. Continue: [next step]
```

## Step 3: Update WIP

Update `.ccc/WIP.md` with current state.

## Difference from /ccc

| | /forward | /ccc |
|---|----------|------|
| Weight | Light | Full |
| Use | Pre-clear | Task switch |
| Detail | Summary | Complete |

## Output

```
✅ Forward saved: #XX
WIP updated
Safe to /clear

To resume: /recap
```
