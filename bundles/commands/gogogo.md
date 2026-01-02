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

**Just run `/gogogo` - it finds and executes the latest plan automatically.**

## How It Works

```
/gogogo
  │
  ├─→ Find open plan issue ──→ None? → "No plan found. Run /nnn first"
  │
  ├─→ Read plan steps from issue
  │
  ├─→ Execute each step (with progress updates)
  │
  ├─→ Test & verify
  │
  └─→ Commit, push, create PR → "✅ Done! PR #X ready for review"
```

## Usage

```bash
# Execute latest plan (most common)
/gogogo

# Execute specific plan
/gogogo #15

# Continue from where you left off
/gogogo --continue
```

## What Happens

### Step 1: Find Plan (Auto)

```bash
gh issue list --search "plan:" --state open --limit 1
```

**If no plan:**
```
❌ No open plan found.

Run /nnn "your task" to create one.
```

**If multiple plans:**
```
⚠️  Multiple plans found:
  #15 - plan: Add authentication
  #12 - plan: Fix API bug

Which one? /gogogo #15 or /gogogo #12
```

### Step 2: Parse & Show Plan

```
📋 Executing Plan #15: "Add authentication"

Steps:
  □ 1. Install next-auth package
  □ 2. Create auth configuration
  □ 3. Add login page
  □ 4. Add middleware
  □ 5. Test login flow

Starting...
```

### Step 3: Execute Each Step

For each step:
1. **Announce** what's being done
2. **Execute** the change
3. **Verify** it works
4. **Mark done** and continue

```
[1/5] Installing next-auth package...
      → npm install next-auth
      ✓ Done

[2/5] Creating auth configuration...
      → Creating src/lib/auth.ts
      ✓ Done

[3/5] Adding login page...
      → Creating src/app/login/page.tsx
      ✓ Done
```

### Step 4: Test & Verify

```bash
# Auto-detect and run tests
npm run build 2>&1 || yarn build 2>&1 || pnpm build 2>&1
npm test 2>&1 || echo "No tests configured"
```

**If build fails:**
```
❌ Build failed. Fixing...
   Error: Missing import in auth.ts
   → Adding missing import
   → Retrying build...
   ✓ Build passed
```

### Step 5: Commit & PR

```bash
# Create branch if needed
git checkout -b feat/[plan-number]-[slug]

# Commit
git add -A
git commit -m "feat: [plan title]

Implements plan from #[number]

Changes:
- [list of changes]

Closes #[plan-number]"

# Push and create PR
git push -u origin [branch]
gh pr create --title "[title]" --body "Implements #[number]"
```

### Step 6: Close Plan Issue

```bash
gh issue close [number] --comment "✅ Implemented in PR #XX"
```

## Output

```
✅ Plan #15 executed successfully!

Completed:
  ✓ Install next-auth package
  ✓ Create auth configuration
  ✓ Add login page
  ✓ Add middleware
  ✓ Test login flow

Changes:
  + src/lib/auth.ts (new)
  + src/app/login/page.tsx (new)
  + src/middleware.ts (new)
  ~ package.json (modified)

Build: ✓ Passed
Tests: ✓ 12 passed

Branch: feat/15-add-authentication
Commit: abc1234
PR: #16 (ready for review)

Plan #15 closed.
```

## Edge Cases

| Situation | What Happens |
|-----------|--------------|
| No plan exists | Suggests `/nnn` |
| Plan already done | Asks to close it or skip |
| Build fails | Auto-fix attempt, then ask for help |
| Step unclear | Asks for clarification |
| Multiple plans | Asks which one to execute |

## Quick Reference

| You want to... | Command |
|----------------|---------|
| Execute latest plan | `/gogogo` |
| Execute specific plan | `/gogogo #15` |
| Continue interrupted | `/gogogo --continue` |
| Create new plan | `/nnn "task"` |
| Check status | `/lll` |
