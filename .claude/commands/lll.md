---
description: List project status - issues, PRs, commits, branches
allowed-tools:
  - Bash
  - Read
---

# LLL - List Project Status

Quick overview of current project state.

## Execute (Parallel)

Run all commands in parallel:

```bash
git status --short
git branch --show-current
git log --oneline -10
gh issue list --limit 10 --state open
gh pr list --limit 5 --state open
```

## Output Format

```markdown
## Project Status

### Branch
`feature/xyz` (+3 ahead of main)

### Changes
- M  src/file.ts
- A  src/new.ts

### Open Issues (3)
| # | Title | Labels |
|---|-------|--------|
| 5 | plan: Add feature | plan |
| 4 | context: Session | context |
| 3 | Bug: Fix login | bug |

### Open PRs (1)
| # | Title | Status |
|---|-------|--------|
| 2 | feat: New feature | Review |

### Recent Commits
- abc1234 feat: Add component
- def5678 fix: Resolve bug

### Suggested Action
[Based on status - e.g., "Ready to /gogogo" or "Run /nnn to plan"]
```

## Quick Mode

Minimal output:
```
Branch: feature/xyz | Changes: 3 | Issues: 2 | PRs: 1
```
