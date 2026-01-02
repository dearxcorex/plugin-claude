---
description: Smart planning - auto-ccc check + create implementation plan (project)
allowed-tools:
  - Bash
  - Read
  - Task
  - Glob
  - Grep
---

# NNN - Smart Planning

**ACTION REQUIRED: Spawn the planner agent immediately.**

## Step 1: Quick Context Check

Run this first:
```bash
gh issue list --label "context" --state open --limit 1
```

If no recent context exists → run `/ccc` first, then continue.

## Step 2: Determine Target

Parse the command argument:
- `/nnn` → Find most recent open issue to plan
- `/nnn #123` → Plan for issue #123
- `/nnn "description"` → Plan for the described task

## Step 3: SPAWN PLANNER AGENT

**YOU MUST use the Task tool now:**

```
Task tool parameters:
  subagent_type: "planner"
  model: "sonnet"
  prompt: |
    Create an implementation plan for: [TARGET]

    Instructions:
    1. Research the codebase thoroughly using Glob, Grep, Read
    2. Identify relevant files and existing patterns
    3. Create a detailed step-by-step plan
    4. After research, create a GitHub issue:

    gh issue create --title "plan: [Task]" --body "$(cat <<'EOF'
    # Implementation Plan: [Task]

    **Created**: [timestamp] GMT+7

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

    ## Success Criteria
    - [ ] [outcome]
    EOF
    )"

    5. Return the issue number created
```

## Expected Output

After agent completes:
```
✅ Plan created: #XX
Ready to /gogogo
```
