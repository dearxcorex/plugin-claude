---
description: Show current work in progress
allowed-tools:
  - Bash
  - Read
  - Write
---

# WIP - Work In Progress

Display and update current work status.

## Usage

- `/wip` → Show current WIP
- `/wip "Working on auth"` → Update focus
- `/wip done` → Mark complete
- `/wip clear` → Clear WIP

## Step 1: Check WIP File

```bash
cat .ccc/WIP.md 2>/dev/null || echo "No WIP file"
git status --short
```

## Step 2: Display

```markdown
## Work In Progress

**Focus**: [from WIP.md]
**Branch**: `feature/xyz`
**Updated**: [timestamp]

### Uncommitted Changes
- M  src/file.ts
- A  src/new.ts

### Active Tasks
- [ ] Task 1
- [ ] Task 2

### Related
- Issue: #XX
- Plan: #XX
```

## Step 3: Update (if argument provided)

Update `.ccc/WIP.md`:

```markdown
# Work In Progress

**Updated**: [timestamp]
**Focus**: [user provided]

## Active Tasks
- [ ] [inferred from focus]

## Changes
[from git status]
```

## Quick Output

```
WIP: [focus] | Branch: feature/xyz | Changes: 3
```
