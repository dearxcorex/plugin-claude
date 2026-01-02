---
description: Minimal setup - memory directory only
allowed-tools:
  - Bash
  - Write
---

# Soul Lite - Minimal Setup

Create only essential memory structure. Quick setup for existing projects.

## Configuration

Default: `.ccc/`

Custom: `/soul-lite mydir` → creates `mydir/memory/`

For nat-agents-core style: `/soul-lite ψ` → creates `ψ/memory/`

## What This Creates

```
.ccc/
└── memory/
    ├── retrospectives/
    └── learnings/
```

## Step 1: Create Structure

```bash
SOUL_DIR="${1:-.ccc}"
mkdir -p "$SOUL_DIR/memory/retrospectives" "$SOUL_DIR/memory/learnings"
touch "$SOUL_DIR/memory/retrospectives/.gitkeep"
touch "$SOUL_DIR/memory/learnings/.gitkeep"
```

## Step 2: Add to .gitignore (optional)

If you don't want to track memory files:

```bash
echo "# CCC memory (optional - remove to track)" >> .gitignore
echo ".ccc/memory/context/" >> .gitignore
```

## When to Use

- Quick setup for existing projects
- Don't need full HOME.md/WIP.md structure
- Just want retrospective storage
- Testing the workflow

## Output

```
✅ Soul lite initialized: .ccc/memory/
- retrospectives/
- learnings/

Run /awaken to install commands
Run /soul-init for full structure later
```

## Upgrade to Full

To upgrade later:

```bash
/soul-init
```

This will add HOME.md, WIP.md, DECISIONS.md, PATTERNS.md without affecting existing memory files.
