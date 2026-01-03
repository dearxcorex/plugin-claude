---
description: Install CCC workflow commands and agents to your project
allowed-tools:
  - Bash
  - Read
  - Write
---

# Awaken - One Command Setup

**Just run `/awaken` and you're ready to go!**

## Usage

```bash
# Standard setup (recommended)
/awaken

# Full setup with project docs + templates
/awaken --full

# Custom memory directory
/awaken --dir .soul
```

## What It Does

```
/awaken
  │
  ├─→ Install 12 commands to .claude/commands/
  │
  ├─→ Install 5 agents to .claude/agents/
  │
  ├─→ Create .ccc/memory/ for retrospectives
  │
  └─→ Create .ccc/templates/ for document templates
```

**With `--full`:**
```
/awaken --full
  │
  ├─→ Install commands + agents
  │
  └─→ Create .ccc/ with:
      ├── HOME.md        (project overview)
      ├── WIP.md         (work in progress)
      ├── DECISIONS.md   (architecture decisions)
      ├── templates/     (document templates)
      │   └── govdoc/    (Thai government docs)
      └── memory/
          ├── retrospectives/
          └── learnings/
```

## Step 1: Find Plugin Source

```bash
PLUGIN_DIR=$(ls -d ~/.claude/plugins/cache/*/ccc-workflow/*/ 2>/dev/null | sort -V | tail -1)
```

## Step 2: Install Commands & Agents

```bash
# Create directories
mkdir -p .claude/commands .claude/agents

# Copy from plugin
cp "$PLUGIN_DIR"bundles/commands/*.md .claude/commands/
cp "$PLUGIN_DIR"bundles/agents/*.md .claude/agents/
```

## Step 3: Create Directory Structure

```bash
# Default directory name (or use --dir argument)
DIR_NAME=".ccc"

# Create all directories
mkdir -p "$DIR_NAME/memory/retrospectives"
mkdir -p "$DIR_NAME/memory/learnings"
mkdir -p "$DIR_NAME/templates/govdoc"
mkdir -p "$DIR_NAME/docs"

# Add .gitkeep to preserve empty dirs
touch "$DIR_NAME/memory/retrospectives/.gitkeep"
touch "$DIR_NAME/memory/learnings/.gitkeep"
touch "$DIR_NAME/templates/.gitkeep"
touch "$DIR_NAME/docs/.gitkeep"
```

## Step 4: (If --full) Create Project Docs

Only if `--full` flag is used:

```bash
# HOME.md - Project overview
cat > "$DIR_NAME/HOME.md" << 'EOF'
# Project Home

## Overview
[Brief description of this project]

## Quick Start
```bash
/lll          # See status
/nnn "task"   # Plan something
/gogogo       # Execute plan
```

## Architecture
[Key technical decisions]

## Links
- Repo: [url]
- Docs: [url]
EOF

# WIP.md - Current work
cat > "$DIR_NAME/WIP.md" << 'EOF'
# Work In Progress

## Current Focus
[What's being worked on now]

## Recent
- [Recent item 1]
- [Recent item 2]

## Blocked
[Any blockers]
EOF

# DECISIONS.md - Architecture decisions
cat > "$DIR_NAME/DECISIONS.md" << 'EOF'
# Architecture Decisions

## Template
### [Decision Title]
**Date**: YYYY-MM-DD
**Status**: [Proposed | Accepted | Deprecated]

**Context**: Why this decision was needed

**Decision**: What was decided

**Consequences**: What this means
EOF
```

## Step 5: (If --full) Create Default Templates

```bash
# Thai Government Memo Template
cat > "$DIR_NAME/templates/govdoc/memo.md" << 'EOF'
# บันทึกข้อความ

**ส่วนราชการ**: {{DEPARTMENT}}
**ที่**: {{DOC_NUMBER}}
**วันที่**: {{DATE}}

**เรื่อง**: {{SUBJECT}}

**เรียน**: {{RECIPIENT}}

{{CONTENT}}

จึงเรียนมาเพื่อโปรด{{ACTION}}

{{SIGNATURE}}
({{NAME}})
{{POSITION}}
EOF

# Thai Government External Letter Template
cat > "$DIR_NAME/templates/govdoc/external.md" << 'EOF'
# หนังสือภายนอก

**ที่**: {{ORG_CODE}}/{{YEAR}}
**ส่วนราชการ**: {{DEPARTMENT}}

**วันที่**: {{DATE}}

**เรื่อง**: {{SUBJECT}}

**เรียน**: {{RECIPIENT}}

**สิ่งที่ส่งมาด้วย**: {{ATTACHMENTS}}

{{CONTENT}}

จึงเรียนมาเพื่อโปรด{{ACTION}}

ขอแสดงความนับถือ

{{SIGNATURE}}
({{NAME}})
{{POSITION}}

{{CONTACT_DEPARTMENT}}
โทร. {{PHONE}}
EOF
```

## Output

**Standard (`/awaken`):**
```
✅ CCC Workflow installed!

Commands (12): .claude/commands/
  Core:      ccc, nnn, gogogo, lll
  Context:   rrr, wip, recap, forward
  Research:  research, review
  Document:  template, mcp-setup

Agents (5): .claude/agents/
  planner, executor, context-finder, researcher, document

Directories: .ccc/
  memory/       (retrospectives, learnings)
  templates/    (document templates)
  docs/         (generated documents)

Ready! Try: /nnn "your first task"
```

**Full (`/awaken --full`):**
```
✅ CCC Workflow installed!

Commands (12): .claude/commands/
Agents (5): .claude/agents/

Project structure: .ccc/
  HOME.md, WIP.md, DECISIONS.md
  templates/govdoc/  (Thai gov document templates)
  memory/            (retrospectives, learnings)
  docs/              (generated documents)

Ready! Try: /nnn "your first task"
```

## After Setup

Your project structure:
```
your-project/
├── .claude/
│   ├── commands/      ← 12 workflow commands
│   └── agents/        ← 5 specialized agents
├── .ccc/
│   ├── HOME.md        ← (only with --full)
│   ├── WIP.md         ← (only with --full)
│   ├── DECISIONS.md   ← (only with --full)
│   ├── templates/     ← document templates
│   │   └── govdoc/    ← Thai government docs
│   ├── docs/          ← generated documents
│   └── memory/
│       ├── retrospectives/
│       └── learnings/
└── your code...
```

## Next Steps

After `/awaken`, just use:
```bash
/nnn "Add user login"    # Plan a task
/gogogo                   # Execute it
```

For document projects:
```bash
/template list           # See available templates
/mcp-setup documents     # Setup document MCP
```

That's it! No other setup needed.
