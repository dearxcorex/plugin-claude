---
name: init-lite
description: Minimal setup - just memory directory for retrospectives
---

# Init Lite - Minimal Setup

Create only the essential memory structure for retrospectives and learnings.

## What This Creates

```
your-project/
└── .ccc/
    └── memory/
        ├── retrospectives/
        └── learnings/
```

## When to Use

- Quick setup for existing projects
- Don't need full HOME.md/WIP.md structure
- Just want retrospective storage

## Instructions

1. **Create minimal structure**:
   ```bash
   mkdir -p .ccc/memory/retrospectives .ccc/memory/learnings
   ```

2. **Create .gitkeep files** to preserve empty directories

3. **Confirm creation** and suggest `/awaken` if commands not installed

## Configuration

Like `/init`, accepts custom directory name:
- `/init-lite` → Creates `.ccc/memory/`
- `/init-lite .soul` → Creates `.soul/memory/`
