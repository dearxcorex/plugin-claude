---
description: Setup project philosophy and knowledge base
allowed-tools:
  - Bash
  - Read
  - Write
---

# Oracle Init - Setup Project Knowledge

Initialize project knowledge base with philosophy and writing style guides.

## What This Creates

```
.claude/
├── knowledge/
│   ├── philosophy.md      ← Project principles
│   └── writing-style.md   ← Documentation style
└── settings.json          ← Project settings
```

## Step 1: Create Knowledge Directory

```bash
mkdir -p .claude/knowledge
```

## Step 2: Create Philosophy Guide

Write `.claude/knowledge/philosophy.md`:

```markdown
# Project Philosophy

## Core Principles

1. **Simplicity First**
   - Prefer simple solutions over complex ones
   - Only add complexity when necessary
   - Code should be self-documenting

2. **Safety Always**
   - Never use force flags
   - Always backup before destructive operations
   - Test before committing

3. **Iterative Progress**
   - Small, focused commits
   - One feature per PR
   - Continuous improvement

4. **Clear Communication**
   - Write descriptive commit messages
   - Document decisions
   - Keep retrospectives

## Anti-Patterns to Avoid

- Over-engineering
- Premature optimization
- Skipping tests
- Force-pushing

## Decision Framework

When making choices:
1. Does it solve the problem simply?
2. Is it safe and reversible?
3. Will it be maintainable?
4. Is it well-documented?
```

## Step 3: Create Writing Style Guide

Write `.claude/knowledge/writing-style.md`:

```markdown
# Writing Style Guide

## Commit Messages

Format:
```
type: brief description

- What: specific changes
- Why: motivation

Closes #XX
```

Types: feat, fix, docs, refactor, test, chore

## Code Comments

- Only when logic isn't obvious
- Explain "why" not "what"
- Keep concise

## Documentation

- Use markdown
- Include examples
- Keep updated

## PR Descriptions

- Reference issue
- List changes
- Include test plan
```

## Step 4: Create Settings

Write `.claude/settings.json`:

```json
{
  "workflow": {
    "workDir": ".ccc",
    "timezone": "GMT+7",
    "autoContext": true
  },
  "safety": {
    "confirmDestructive": true,
    "backupBeforeDelete": true
  }
}
```

## Output

```
✅ Oracle initialized
- .claude/knowledge/philosophy.md
- .claude/knowledge/writing-style.md
- .claude/settings.json

Run /awaken to install commands
Run /soul-lite to create memory structure
```
