---
name: init
description: Setup full CCC project structure with memory and templates
---

# Init - Full Project Setup

Create the complete CCC workflow structure in your project.

## What This Creates

```
your-project/
├── .claude/
│   ├── commands/     ← (use /awaken to populate)
│   ├── agents/       ← (use /awaken to populate)
│   └── settings.json
└── .ccc/             ← Workflow directory (configurable)
    ├── HOME.md       ← Project overview & quick links
    ├── WIP.md        ← Current work in progress
    ├── DECISIONS.md  ← Architecture decisions log
    └── memory/
        ├── retrospectives/   ← Session retrospectives
        ├── learnings/        ← Captured learnings
        └── context/          ← Context snapshots
```

## Configuration

**Default directory**: `.ccc/`

User can specify custom directory name:
- `/init` → Creates `.ccc/`
- `/init myworkflow` → Creates `myworkflow/`
- `/init .soul` → Creates `.soul/` (nat-agents-core style)

## Instructions

1. **Ask user** for preferred directory name (default: `.ccc`)
2. **Create directory structure** as shown above
3. **Create HOME.md** with project info template
4. **Create WIP.md** with empty work-in-progress template
5. **Create DECISIONS.md** for architecture decision records
6. **Create memory subdirectories**

## Templates

### HOME.md Template
```markdown
# Project Home

**Project**: [project-name]
**Created**: [date]
**Last Updated**: [date]

## Quick Links
- [Current WIP](./WIP.md)
- [Decisions](./DECISIONS.md)
- [Recent Retrospectives](./memory/retrospectives/)

## Project Overview
[Brief description of the project]

## Key Commands
- `/ccc` - Save context and compact
- `/nnn` - Create implementation plan
- `/gogogo` - Execute the plan
- `/lll` - See project status
- `/rrr` - Write retrospective
```

### WIP.md Template
```markdown
# Work In Progress

**Last Updated**: [timestamp]
**Current Focus**: [none]

## Active Tasks
- [ ] No active tasks

## Recent Changes
[none yet]

## Blockers
[none]

## Next Steps
1. Run `/lll` to see project status
2. Run `/nnn` to plan next task
```

## After Init

Suggest user run:
1. `/awaken` to install commands and agents
2. `/lll` to see current project status
