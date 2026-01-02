---
description: Create session retrospective
allowed-tools:
  - Bash
  - Read
  - Write
  - Task
---

# RRR - Session Retrospective

Document session activities, learnings, and outcomes.

## CRITICAL: Required Sections

**AI Diary** and **Honest Feedback** are **MANDATORY** (100+ words each).
Never skip these sections.

## Step 1: Gather Data

```bash
git diff --name-only main...HEAD
git log --oneline main...HEAD
date '+%Y-%m-%d %H:%M'
```

## Step 2: Create Retrospective

Save to `.ccc/memory/retrospectives/YYYY-MM/DD_HHMM_slug.md`:

```markdown
# Session Retrospective

**Date**: YYYY-MM-DD
**Time**: HH:MM - HH:MM GMT+7
**Duration**: ~X minutes
**Focus**: [brief description]
**Issue**: #XX
**PR**: #XX

## Summary
[2-3 sentences of what was accomplished]

## Timeline
- HH:MM - Started
- HH:MM - [Event]
- HH:MM - Completed

## Files Modified
[list from git diff]

## AI Diary (Required - 100+ words)

[First-person narrative:
- Initial assumptions
- How approach evolved
- Moments of confusion/clarity
- What surprised you
- Honest reflection on the work]

## What Went Well
- [success 1]
- [success 2]

## What Could Improve
- [area 1]

## Honest Feedback (Required - 100+ words)

[Frank assessment:
- Session effectiveness
- What frustrated you
- What worked well
- Suggestions for improvement]

## Lessons Learned
- **Pattern**: [description]
- **Discovery**: [what learned]

## Next Steps
- [ ] [task 1]
- [ ] [task 2]
```

## Step 3: Commit & Link

```bash
git add .ccc/memory/retrospectives/
git commit -m "docs: Add session retrospective"
gh issue comment XX --body "Retrospective: .ccc/memory/retrospectives/[file]"
```

## Output

```
✅ Retrospective saved: .ccc/memory/retrospectives/[file]
Linked to issue #XX
```
