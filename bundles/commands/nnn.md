---
description: Smart planning - auto-ccc check + create implementation plan (project)
allowed-tools:
  - Bash
  - Read
  - Write
  - Task
  - Glob
  - Grep
---

# NNN - Smart Planning (Start Here!)

**This is your main entry point.** Just run `/nnn` and it handles everything.

## How It Works

```
/nnn "Add user login"
  │
  ├─→ Check: GitHub repo exists? ──→ No → Error: "Init git repo first"
  │
  ├─→ Check: Any open plan? ──→ Yes → "Plan #X exists. /gogogo to execute or /nnn --new to create new"
  │
  ├─→ Gather context automatically (git status, recent commits, open issues)
  │
  ├─→ Spawn planner agent to research codebase
  │
  └─→ Create plan issue → "✅ Plan #X created. Ready to /gogogo"
```

## Usage

```bash
# Plan something new (most common)
/nnn "Add dark mode toggle"
/nnn "Fix login bug on Safari"
/nnn "Refactor API to use REST"

# Plan for existing issue
/nnn #42

# Force new plan (even if one exists)
/nnn --new "Different approach"
```

## What Happens

### Step 1: Pre-flight Checks (Auto)

Run silently:
```bash
git rev-parse --git-dir 2>/dev/null  # Check if git repo
gh issue list --limit 1 2>/dev/null   # Check if GitHub connected
gh issue list --search "plan:" --state open --limit 1  # Check existing plans
```

**If existing open plan found:**
```
⚠️  Open plan exists: #5 "plan: Add authentication"

Options:
1. /gogogo     → Execute this plan
2. /nnn --new  → Create different plan
3. Close #5 first: gh issue close 5
```

### Step 2: Auto-Gather Context

No need for `/ccc` first! `/nnn` gathers context automatically:

```bash
# Run in parallel
git status --short
git log --oneline -5
git branch --show-current
gh issue list --limit 5 --state open
```

### Step 3: Spawn Planner Agent

```
Task tool:
  subagent_type: "planner"
  prompt: |
    Create implementation plan for: [USER REQUEST]

    Current context:
    - Branch: [branch]
    - Recent commits: [commits]
    - Open issues: [issues]

    Instructions:
    1. Research codebase with Glob, Grep, Read
    2. Find relevant files and patterns
    3. Create step-by-step plan
    4. Create GitHub issue with plan
```

### Step 4: Create Plan Issue

```bash
gh issue create --title "plan: [Task]" --body "$(cat <<'EOF'
# Implementation Plan: [Task]

**Created**: [timestamp] GMT+7
**Context**: Branch `[branch]`, [X] open issues

## Problem Statement
[what needs to be done]

## Research Summary
### Relevant Files
- `path/file` - [why relevant]

### Existing Patterns
- [pattern found]

## Implementation Steps

### Phase 1: [Name]
- [ ] Step 1.1
- [ ] Step 1.2

### Phase 2: [Name]
- [ ] Step 2.1

## Success Criteria
- [ ] [measurable outcome]

## Notes
- [any warnings or considerations]
EOF
)"
```

## Output

```
✅ Plan created: #12
   "plan: Add dark mode toggle"

Context gathered:
  - Branch: main
  - 3 recent commits
  - 2 open issues

Research found:
  - src/styles/theme.ts (existing theme system)
  - src/components/Settings.tsx (where to add toggle)

Ready to /gogogo
```

## Quick Reference

| You want to... | Command |
|----------------|---------|
| Plan new task | `/nnn "description"` |
| Plan existing issue | `/nnn #42` |
| Force new plan | `/nnn --new "description"` |
| Execute plan | `/gogogo` |
| Check status | `/lll` |
