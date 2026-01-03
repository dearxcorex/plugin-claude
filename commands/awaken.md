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

# Full setup with project docs
/awaken --full

# Custom memory directory
/awaken --dir .soul
```

## What It Does

```
/awaken
  │
  ├─→ Install 10 commands to .claude/commands/
  │
  ├─→ Install 4 agents to .claude/agents/
  │
  └─→ Create .ccc/memory/ for retrospectives
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

# Create directories
mkdir -p "$DIR_NAME/memory/retrospectives"
mkdir -p "$DIR_NAME/memory/learnings"

# Add .gitkeep to preserve empty dirs
touch "$DIR_NAME/memory/retrospectives/.gitkeep"
touch "$DIR_NAME/memory/learnings/.gitkeep"
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

## Output

**Standard (`/awaken`):**
```
✅ CCC Workflow installed!

Commands (10): .claude/commands/
  Core:      ccc, nnn, gogogo, lll
  Context:   rrr, wip, recap, forward
  Research:  research, review

Agents (4): .claude/agents/
  planner, executor, context-finder, researcher

Directories: .ccc/
  memory/  (retrospectives, learnings)

Ready! Try: /nnn "your first task"
```

**Full (`/awaken --full`):**
```
✅ CCC Workflow installed!

Commands (10): .claude/commands/
Agents (4): .claude/agents/

Project structure: .ccc/
  HOME.md, WIP.md, DECISIONS.md
  memory/  (retrospectives, learnings)

Ready! Try: /nnn "your first task"
```

## After Setup

Your project structure:
```
your-project/
├── .claude/
│   ├── commands/      ← 10 workflow commands
│   └── agents/        ← 4 specialized agents
├── .ccc/
│   ├── HOME.md        ← (only with --full)
│   ├── WIP.md         ← (only with --full)
│   ├── DECISIONS.md   ← (only with --full)
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

That's it! No other setup needed.
