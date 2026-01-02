---
description: Execute the most recent implementation plan
allowed-tools:
  - Bash
  - Read
  - Write
  - Edit
  - Task
  - Glob
  - Grep
---

# GOGOGO - Execute Plan

Find and execute the most recent `plan:` issue step by step.

## Step 1: Find Plan Issue

```bash
gh issue list --search "plan:" --state open --limit 1
```

If no plan found → suggest `/nnn` first.

## Step 2: Parse Plan

Read issue, extract:
- Implementation steps (checkboxes)
- Files to modify
- Success criteria

## Step 3: Execute Steps

For each step:

1. **Announce**: "Starting: [step]"
2. **Execute**: Make code changes
3. **Verify**: Check it works
4. **Comment**: Update issue progress

Use `executor` agent for complex changes:
```
Task: subagent_type=executor
Execute step: [description]
```

## Step 4: Test

```bash
npm run build  # or relevant build command
npm test       # or relevant test command
```

Fix any failures before continuing.

## Step 5: Commit & PR

```bash
git add -A
git commit -m "feat: [description]

Implements plan from #XX

- [change 1]
- [change 2]

Closes #XX"

git push -u origin [branch]
gh pr create --title "[title]" --body "Implements #XX"
```

## Step 6: Close Plan

```bash
gh issue close [plan-issue] --comment "✅ Implemented in PR #XX"
```

## Output

```
✅ Plan #XX executed
- X/X steps completed
- Tests: passing
- PR: #XX
```
