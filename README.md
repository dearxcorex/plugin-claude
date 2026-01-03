# CCC - Claude Code Companion

AI-powered workflow automation for Claude Code. Plan, execute, and track your development tasks.

---

## Install

```bash
/plugin marketplace add dearxcorex/plugin-claude
/plugin install ccc@dearxcorex-plugin-claude
```

Done! Commands available as `/ccc:nnn`, `/ccc:gogogo`, etc.

---

## Start Working

### The Core Loop

```
/ccc:nnn "task"  →  /ccc:gogogo  →  Done!
```

That's it. Two commands for most work.

---

## All Commands

### Core Commands (Use Daily)

| Command | What it does |
|---------|--------------|
| `/ccc:nnn "task"` | Plan a task - AI researches your code and creates a GitHub issue |
| `/ccc:gogogo` | Execute the plan - AI follows the steps, writes code, creates PR |
| `/ccc:lll` | Show status - open issues, PRs, recent commits |

### Context Commands

| Command | What it does |
|---------|--------------|
| `/ccc:ccc` | Save context to GitHub issue (before breaks) |
| `/ccc:recap` | Get summary of current work (starting new session) |
| `/ccc:wip` | Show what's in progress |
| `/ccc:forward` | Forward context before `/clear` |
| `/ccc:rrr` | Write session retrospective |

### Research Commands

| Command | What it does |
|---------|--------------|
| `/ccc:research <url>` | Analyze a website or documentation |
| `/ccc:research github:user/repo` | Analyze a GitHub repository |
| `/ccc:review` | Review your current project |
| `/ccc:review security` | Security-focused review |

---

## Tutorial: Your First Feature

Let's add a dark mode toggle to a React app.

### 1. Check Status

```bash
/ccc:lll
```

Output:
```
Branch: main (clean)
Open Issues: 0
Open PRs: 0
```

### 2. Plan the Feature

```bash
/ccc:nnn "Add dark mode toggle to the header"
```

**What happens:**
- AI scans your codebase
- Finds relevant files (Header.tsx, styles, etc.)
- Creates GitHub issue #1 with implementation plan

Output:
```
✅ Plan created: #1 "plan: Add dark mode toggle"

Found:
  - src/components/Header.tsx
  - src/styles/globals.css
  - No theme system exists

Steps planned:
  1. Create ThemeContext
  2. Add toggle button to Header
  3. Implement dark styles
  4. Persist preference

Ready to /ccc:gogogo
```

### 3. Execute the Plan

```bash
/ccc:gogogo
```

**What happens:**
- AI follows each step
- Creates/modifies files
- Runs build to verify
- Creates commit and PR

Output:
```
✅ Plan #1 executed!

Created:
  + src/context/ThemeContext.tsx
  + src/components/ThemeToggle.tsx

Modified:
  ~ src/components/Header.tsx
  ~ src/styles/globals.css

Build: ✓ Passed
PR: #2 ready for review
```

### 4. Done!

Check your PR at the link provided. Review, merge, ship.

---

## Tutorial: Multi-Day Feature

For bigger features that span multiple sessions.

### Day 1: Start

```bash
/ccc:nnn "Build user authentication system"
/ccc:gogogo
```

Work gets partially done. Before you leave:

```bash
/ccc:ccc
```

Saves context to GitHub issue #X.

### Day 2: Continue

```bash
/ccc:recap
```

Shows where you left off:
```
Current: feat/auth branch
Last: Completed login form
Next: Add JWT validation
```

Continue:
```bash
/ccc:gogogo
```

### Day 3: Finish

```bash
/ccc:gogogo    # Complete the work
/ccc:rrr       # Write retrospective
```

---

## Tutorial: Research Before Building

When you need to understand something first.

### Research a Library

```bash
/ccc:research github:shadcn/ui
```

Output:
```
## shadcn/ui

TypeScript component library using:
- Radix UI primitives
- Tailwind CSS
- cn() utility for class merging

Key files:
- components/ui/*.tsx
- lib/utils.ts

Pattern: Copy components, not install
```

### Research Documentation

```bash
/ccc:research https://nextjs.org/docs/app/api-reference/functions/cookies
```

### Then Build

```bash
/ccc:nnn "Add shadcn button component following their patterns"
/ccc:gogogo
```

---

## Tutorial: Review Your Code

### Quick Review

```bash
/ccc:review
```

Output:
```
## Project Health: 7/10

Strengths:
✓ TypeScript strict mode
✓ Good folder structure

Issues:
⚠ 5 TODO comments
⚠ Missing error boundaries
⚠ No tests for utils/

Suggestions:
1. Add error boundaries to pages
2. Write tests for date utilities
```

### Security Review

```bash
/ccc:review security
```

Focuses on:
- Input validation
- Authentication flows
- SQL/XSS vulnerabilities
- Exposed secrets

---

## Daily Workflow

```bash
# Morning
/ccc:lll                # What's the status?
/ccc:recap              # What was I doing?

# Working
/ccc:nnn "description"  # Plan it
/ccc:gogogo             # Build it

# Before breaks
/ccc:ccc                # Save context

# End of day
/ccc:rrr                # Retrospective
```

---

## The Agents

Your plugin includes 4 AI agents:

| Agent | Purpose |
|-------|---------|
| **planner** | Researches codebase, creates detailed plans |
| **executor** | Follows plans, writes code safely |
| **context-finder** | Fast codebase search |
| **researcher** | Web research, GitHub analysis |

Each agent has restricted permissions for safety.

---

## Tips

**Do:**
- Always `/ccc:nnn` before coding (plans help!)
- Use `/ccc:ccc` before long breaks
- Run `/ccc:lll` to stay oriented

**Don't:**
- Skip planning for "quick" changes
- Forget to save context
- Ignore the retrospective

---

## Troubleshooting

### Command not found

```bash
/plugin marketplace add dearxcorex/plugin-claude
/plugin install ccc@dearxcorex-plugin-claude
```

### Plugin not updating

```bash
/plugin uninstall ccc@dearxcorex-plugin-claude
/plugin marketplace add dearxcorex/plugin-claude
/plugin install ccc@dearxcorex-plugin-claude
```

---

## Quick Reference

```bash
# Install (once)
/plugin marketplace add dearxcorex/plugin-claude
/plugin install ccc@dearxcorex-plugin-claude

# Daily use
/ccc:lll                  # Status
/ccc:nnn "task"           # Plan
/ccc:gogogo               # Execute
/ccc:ccc                  # Save context
/ccc:rrr                  # Retrospective

# Research
/ccc:research <url>       # Analyze site
/ccc:research github:u/r  # Analyze repo
/ccc:review               # Review project
```

---

MIT License | [@dearxcorex](https://github.com/dearxcorex)
