---
description: Install CCC workflow commands and agents to your project
allowed-tools:
  - Bash
  - Read
  - Write
---

# Awaken - Install CCC Workflow

Install all workflow commands and agents to your current project's `.claude/` directory.

## What Gets Installed

**Commands** (8): ccc, nnn, gogogo, lll, rrr, wip, recap, forward

**Agents** (3): context-finder, executor, planner

## Step 1: Verify Plugin Location

First, find the plugin cache location:

```bash
ls -d ~/.claude/plugins/cache/*/ccc-workflow/*/ 2>/dev/null | sort -V | tail -1
```

## Step 2: Install

Run this command to copy all bundles to your project:

```bash
CORE=`ls -d ~/.claude/plugins/cache/*/ccc-workflow/*/ 2>/dev/null | sort -V | tail -1` && mkdir -p .claude/commands .claude/agents && cp "$CORE"bundles/commands/*.md .claude/commands/ && cp "$CORE"bundles/agents/*.md .claude/agents/ && echo "✅ Installed from $CORE"
```

## Step 3: Verify Installation

```bash
echo "Commands:" && ls .claude/commands/*.md 2>/dev/null | wc -l && echo "Agents:" && ls .claude/agents/*.md 2>/dev/null | wc -l
```

## What's Installed

### Commands → `.claude/commands/`
| Command | Purpose |
|---------|---------|
| `/ccc` | Create context issue + compact conversation |
| `/nnn` | Smart planning (auto-ccc check + create plan) |
| `/gogogo` | Execute most recent plan issue |
| `/lll` | List project status (issues, PRs, commits) |
| `/rrr` | Create session retrospective |
| `/wip` | Show current work in progress |
| `/recap` | Fresh start summary for new sessions |
| `/forward` | Forward context before /clear |

### Agents → `.claude/agents/`
| Agent | Model | Purpose |
|-------|-------|---------|
| `context-finder` | haiku | Fast codebase search (read-only) |
| `executor` | sonnet | Execute plans securely |
| `planner` | sonnet | Create implementation plans (research-only) |

## After Installation

Suggest running:
- `/init-lite` to create memory structure
- `/lll` to see project status
- `/recap` to get started

## Upgrade Existing

If commands already exist, the copy will overwrite with latest versions.

To backup first:
```bash
cp -r .claude/commands .claude/commands.backup 2>/dev/null
cp -r .claude/agents .claude/agents.backup 2>/dev/null
```
