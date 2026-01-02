---
description: Create full project structure with memory and templates
allowed-tools:
  - Bash
  - Read
  - Write
---

# Soul Init - Full Project Structure

Create complete workflow structure with all templates.

## Configuration

Default directory: `.ccc/`

Custom: `/soul-init mydir` → creates `mydir/`

For nat-agents-core style: `/soul-init ψ` → creates `ψ/`

## What This Creates

```
.ccc/                      (or custom name)
├── HOME.md                ← Project overview
├── WIP.md                 ← Work in progress
├── DECISIONS.md           ← Architecture decisions
├── PATTERNS.md            ← Code patterns reference
└── memory/
    ├── retrospectives/    ← Session retrospectives
    ├── learnings/         ← Captured learnings
    └── context/           ← Context snapshots
```

## Step 1: Get Directory Name

Check for argument, default to `.ccc`:

```bash
SOUL_DIR="${1:-.ccc}"
```

## Step 2: Create Structure

```bash
mkdir -p "$SOUL_DIR/memory/retrospectives"
mkdir -p "$SOUL_DIR/memory/learnings"
mkdir -p "$SOUL_DIR/memory/context"
```

## Step 3: Create HOME.md

```markdown
# Project Home

**Project**: [name from package.json or directory]
**Created**: [timestamp]
**Updated**: [timestamp]

## Quick Links

- [Current WIP](./WIP.md)
- [Decisions](./DECISIONS.md)
- [Patterns](./PATTERNS.md)
- [Retrospectives](./memory/retrospectives/)

## Overview

[Brief project description]

## Quick Commands

| Command | Purpose |
|---------|---------|
| `/lll` | See status |
| `/nnn` | Plan task |
| `/gogogo` | Execute plan |
| `/ccc` | Save context |
| `/rrr` | Retrospective |

## Current Focus

[What's being worked on]

## Recent Updates

- [date]: [update]
```

## Step 4: Create WIP.md

```markdown
# Work In Progress

**Updated**: [timestamp]
**Focus**: None

## Active Tasks

- [ ] No active tasks

## Uncommitted Changes

None

## Related Issues

None

## Next Steps

1. Run `/lll` to see project status
2. Run `/nnn` to plan next task
```

## Step 5: Create DECISIONS.md

```markdown
# Architecture Decision Records

## Template

### ADR-XXX: [Title]

**Date**: YYYY-MM-DD
**Status**: [Proposed | Accepted | Deprecated]

#### Context
[What is the issue?]

#### Decision
[What was decided?]

#### Consequences
[What are the results?]

---

## Decisions

(No decisions recorded yet)
```

## Step 6: Create PATTERNS.md

```markdown
# Code Patterns

## Template

### Pattern: [Name]

**Use when**: [situation]

**Example**:
```
[code example]
```

**Why**: [rationale]

---

## Patterns

(No patterns recorded yet)
```

## Output

```
✅ Soul initialized: .ccc/
- HOME.md
- WIP.md
- DECISIONS.md
- PATTERNS.md
- memory/retrospectives/
- memory/learnings/
- memory/context/

Run /awaken to install commands
```
