# CCC-Workflow

AI-powered workflow automation for Claude Code. Plan, execute, and track your development tasks.

---

## Step 1: Install the Plugin

Run this once (globally installs to your system):

```bash
/install-plugin github:dearxcorex/plugin-claude
```

---

## Step 2: Setup Your Project

Navigate to any project and run:

```bash
cd your-project
/awaken
```

This creates:
```
your-project/
├── .claude/
│   ├── commands/     ← 10 workflow commands
│   └── agents/       ← 4 AI agents
└── .ccc/
    └── memory/       ← Retrospectives & learnings
```

**Options:**
```bash
/awaken              # Standard setup
/awaken --full       # + HOME.md, WIP.md, DECISIONS.md
/awaken --dir .ai    # Custom directory name instead of .ccc
```

---

## Step 3: Start Working

### The Core Loop

```
/nnn "task"  →  /gogogo  →  Done!
```

That's it. Two commands for most work.

---

## All Commands

### Core Commands (Use Daily)

| Command | What it does |
|---------|--------------|
| `/nnn "task"` | Plan a task - AI researches your code and creates a GitHub issue with implementation steps |
| `/gogogo` | Execute the plan - AI follows the steps, writes code, creates PR |
| `/lll` | Show status - open issues, PRs, recent commits |

### Context Commands (Use When Needed)

| Command | What it does |
|---------|--------------|
| `/ccc` | Save context to GitHub issue (before breaks) |
| `/recap` | Get summary of current work (starting new session) |
| `/wip` | Show what's in progress |
| `/forward` | Forward context before `/clear` |
| `/rrr` | Write session retrospective |

### Research Commands

| Command | What it does |
|---------|--------------|
| `/research <url>` | Analyze a website or documentation |
| `/research github:user/repo` | Analyze a GitHub repository |
| `/research "query"` | Search and research a topic |
| `/review` | Review your current project |
| `/review security` | Security-focused review |

---

## Tutorial: Your First Feature

Let's add a dark mode toggle to a React app.

### 1. Check Status

```bash
/lll
```

Output:
```
Branch: main (clean)
Open Issues: 0
Open PRs: 0
```

### 2. Plan the Feature

```bash
/nnn "Add dark mode toggle to the header"
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

Ready to /gogogo
```

### 3. Execute the Plan

```bash
/gogogo
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
/nnn "Build user authentication system"
/gogogo
```

Work gets partially done. Before you leave:

```bash
/ccc
```

Saves context to GitHub issue #X.

### Day 2: Continue

```bash
/recap
```

Shows where you left off:
```
Current: feat/auth branch
Last: Completed login form
Next: Add JWT validation
```

Continue:
```bash
/gogogo
```

### Day 3: Finish

```bash
/gogogo    # Complete the work
/rrr       # Write retrospective
```

---

## Tutorial: Research Before Building

When you need to understand something first.

### Research a Library

```bash
/research github:shadcn/ui
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
/research https://nextjs.org/docs/app/api-reference/functions/cookies
```

### Research a Topic

```bash
/research "React Server Components best practices 2024"
```

### Then Build

```bash
/nnn "Add shadcn button component following their patterns"
/gogogo
```

---

## Tutorial: Review Your Code

### Quick Review

```bash
/review
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
/review security
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
/lll                    # What's the status?
/recap                  # What was I doing?

# Working
/nnn "description"      # Plan it
/gogogo                 # Build it

# Before breaks
/ccc                    # Save context

# End of day
/rrr                    # Retrospective
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
- Always `/nnn` before coding (plans help!)
- Use `/ccc` before long breaks
- Run `/lll` to stay oriented

**Don't:**
- Skip planning for "quick" changes
- Forget to save context
- Ignore the retrospective

---

## Troubleshooting

### Command not found

```bash
/install-plugin github:dearxcorex/plugin-claude
/awaken
```

### Want to reset

```bash
rm -rf .claude/commands .claude/agents .ccc
/awaken
```

### Plugin not updating

```bash
/uninstall-plugin ccc-workflow
/install-plugin github:dearxcorex/plugin-claude
```

---

## Quick Reference

```bash
# Install (once)
/install-plugin github:dearxcorex/plugin-claude

# Setup (once per project)
/awaken

# Daily use
/lll                      # Status
/nnn "task"               # Plan
/gogogo                   # Execute
/ccc                      # Save context
/rrr                      # Retrospective

# Research
/research <url>           # Analyze site
/research github:u/r      # Analyze repo
/review                   # Review project
```

---

MIT License | [@dearxcorex](https://github.com/dearxcorex)
