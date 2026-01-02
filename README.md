# CCC-Workflow

Claude Code Companion - Workflow automation, context management, and project intelligence.

## What You Get

### Commands

| Command | Purpose |
|---------|---------|
| `/awaken` | Install commands + agents to your project |
| `/oracle-init` | Setup project philosophy & knowledge |
| `/soul-init` | Create full project structure |
| `/soul-lite` | Minimal setup (memory only) |

### What /awaken Installs

**Commands** (to `.claude/commands/`):

| Command | Purpose |
|---------|---------|
| `/ccc` | Create context issue + compact conversation |
| `/nnn` | Smart planning (auto-ccc + create plan) |
| `/gogogo` | Execute most recent plan issue |
| `/lll` | List project status (issues, PRs, commits) |
| `/rrr` | Session retrospective with AI diary |
| `/wip` | Show/update work in progress |
| `/recap` | Fresh start summary for new sessions |
| `/forward` | Forward context before /clear |

**Agents** (to `.claude/agents/`):

| Agent | Model | Purpose |
|-------|-------|---------|
| `context-finder` | haiku | Fast codebase search (read-only) |
| `executor` | sonnet | Execute plans (secure) |
| `planner` | sonnet | Create plans (research-only) |

## Project Structure After Setup

```
your-project/
├── .claude/
│   ├── commands/      ← installed by /awaken
│   ├── agents/        ← installed by /awaken
│   ├── knowledge/     ← created by /oracle-init
│   │   ├── philosophy.md
│   │   └── writing-style.md
│   └── settings.json
└── .ccc/              ← created by /soul-init (configurable)
    ├── HOME.md
    ├── WIP.md
    ├── DECISIONS.md
    ├── PATTERNS.md
    └── memory/
        ├── retrospectives/
        ├── learnings/
        └── context/
```

## Quick Start

```bash
# 1. Install plugin
/install-plugin github:dearxcorex/plugin-claude

# 2. Setup your project
/ccc-workflow:oracle-init    # Philosophy & knowledge
/ccc-workflow:soul-lite      # Or /soul-init for full structure
/ccc-workflow:awaken         # Install commands & agents

# 3. Start working
/recap                       # Get up to speed
/lll                         # See project status
/nnn                         # Plan next task
/gogogo                      # Execute the plan
/rrr                         # Write retrospective
```

## Workflow Pattern

```
/ccc → /nnn → /gogogo → /rrr
  ↓      ↓       ↓        ↓
context  plan   execute  reflect
```

## Directory Configuration

All commands support custom directory names:

```bash
/soul-init           # Creates .ccc/
/soul-init mydir     # Creates mydir/
/soul-init ψ         # Creates ψ/ (nat-agents-core style)
```

## Improvements Over nat-agents-core

| Issue | nat-agents-core | ccc-workflow |
|-------|-----------------|--------------|
| Directory | Forced ψ/ | Configurable |
| Models | Haiku only | Haiku + Sonnet |
| Security | Unrestricted | Tool restrictions |
| Executor | Risky | Safe (no force, no auto-merge) |
| Philosophy | Heavy | Practical |
| Setup | Complex | Simple 3-step |

## Agent Security

All agents have explicit **tool restrictions**:

| Agent | Tools | Cannot |
|-------|-------|--------|
| context-finder | Glob, Grep, Read, LSP | Write, Bash, Web |
| planner | Read, Glob, Grep, LSP, Web | Write, Edit, Bash |
| executor | Read, Write, Edit, Bash, Glob | WebFetch, auto-merge |

## License

MIT

## Author

[@dearxcorex](https://github.com/dearxcorex)
