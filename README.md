# CCC-Workflow

Claude Code Companion - Workflow automation for Claude Code.

## Quick Start (2 Steps!)

```bash
# Step 1: Install plugin (once)
/install-plugin github:dearxcorex/plugin-claude

# Step 2: Setup your project (once per project)
/awaken
```

**Done!** Now use:
```bash
/nnn "Add user login"    # Plan a task
/gogogo                   # Execute it
```

---

## The Simple Flow

```
/nnn → /gogogo → done!
  │        │
  │        └─→ Executes plan, creates PR
  │
  └─→ Researches codebase, creates plan issue
```

---

## Real World Example

### Setup (One Time)

```bash
cd my-project
/awaken
```

Output:
```
✅ CCC Workflow installed!

Commands (8): .claude/commands/
Agents (3): .claude/agents/
Memory: .ccc/memory/

Ready! Try: /nnn "your first task"
```

### Daily Work

```bash
# Plan what you want to do
/nnn "Add dark mode toggle to settings"
```

Output:
```
✅ Plan created: #1
   "plan: Add dark mode toggle"

Research found:
  - src/styles/theme.ts (existing theme)
  - src/components/Settings.tsx (add toggle here)

Ready to /gogogo
```

```bash
# Execute the plan
/gogogo
```

Output:
```
✅ Plan #1 executed!

Completed:
  ✓ Create theme toggle component
  ✓ Add to Settings page
  ✓ Store preference in localStorage
  ✓ Update global styles

PR: #2 (ready for review)
```

---

## All Commands

### Main Commands (Daily Use)

| Command | What It Does |
|---------|--------------|
| `/nnn "task"` | Plan a task (researches codebase, creates issue) |
| `/gogogo` | Execute latest plan (makes changes, creates PR) |
| `/lll` | Show project status (issues, PRs, branches) |

### Context Commands (Optional)

| Command | What It Does |
|---------|--------------|
| `/ccc` | Save context to GitHub issue |
| `/recap` | Get summary of current state |
| `/wip` | Show work in progress |
| `/forward` | Save context before `/clear` |
| `/rrr` | Write session retrospective |

### Setup Command

| Command | What It Does |
|---------|--------------|
| `/awaken` | Install everything (run once per project) |
| `/awaken --full` | Install + create project docs |
| `/awaken --dir .soul` | Use custom directory name |

---

## What `/awaken` Creates

```
your-project/
├── .claude/
│   ├── commands/        ← 8 workflow commands
│   │   ├── nnn.md       (smart planning)
│   │   ├── gogogo.md    (execute plans)
│   │   ├── lll.md       (project status)
│   │   ├── ccc.md       (save context)
│   │   ├── rrr.md       (retrospective)
│   │   ├── wip.md       (work in progress)
│   │   ├── recap.md     (session summary)
│   │   └── forward.md   (forward context)
│   └── agents/          ← 3 specialized agents
│       ├── planner.md   (researches & plans)
│       ├── executor.md  (executes safely)
│       └── context-finder.md (fast search)
└── .ccc/
    └── memory/
        ├── retrospectives/
        └── learnings/
```

---

## Example Workflows

### Feature Development

```bash
/nnn "Add user authentication with OAuth"
/gogogo
# Review PR, merge, done!
```

### Bug Fix

```bash
/nnn "#42"                    # Plan fix for issue #42
/gogogo
```

### Multi-Session Work

```bash
# Session 1
/nnn "Build payment system"
/gogogo                        # Partial progress
/ccc                           # Save context

# Session 2
/recap                         # Catch up
/gogogo                        # Continue
```

### Check What's Happening

```bash
/lll
```

Output:
```
## Project Status

Branch: feat/auth (+3 ahead)

Open Issues (2):
  #5 - plan: Add OAuth
  #3 - bug: Login timeout

Open PRs (1):
  #4 - feat: User registration

Recent Commits:
  abc123 feat: Add signup form
  def456 fix: Validation error
```

---

## Tips

| Do | Don't |
|----|-------|
| `/nnn` before coding | Jump straight into code |
| `/lll` to check status | Guess what's happening |
| `/ccc` before breaks | Lose context |
| `/gogogo` to execute | Manually follow plans |

---

## Comparison: `/awaken` vs `/awaken --full`

| Feature | `/awaken` | `/awaken --full` |
|---------|-----------|------------------|
| Commands | ✓ | ✓ |
| Agents | ✓ | ✓ |
| memory/ | ✓ | ✓ |
| HOME.md | - | ✓ |
| WIP.md | - | ✓ |
| DECISIONS.md | - | ✓ |

Use `--full` if you want project documentation templates.

---

## License

MIT

## Author

[@dearxcorex](https://github.com/dearxcorex)
