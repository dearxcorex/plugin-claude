# CCC-Workflow

Claude Code Companion - Workflow automation for Claude Code.

## Quick Start

```bash
# Step 1: Install plugin (once globally)
/install-plugin github:dearxcorex/plugin-claude

# Step 2: Setup your project
/awaken

# Step 3: Start working!
/nnn "Add user login"
/gogogo
```

---

## `/awaken` - The Setup Command

One command to setup everything. Run once per project.

### Option 1: `/awaken` (Standard)

```bash
/awaken
```

**What it creates:**

```
your-project/
├── .claude/
│   ├── commands/              ← 12 workflow commands
│   │   ├── nnn.md
│   │   ├── gogogo.md
│   │   ├── lll.md
│   │   ├── ccc.md
│   │   ├── rrr.md
│   │   ├── wip.md
│   │   ├── recap.md
│   │   ├── forward.md
│   │   ├── research.md
│   │   ├── review.md
│   │   ├── template.md        ← NEW
│   │   └── mcp-setup.md       ← NEW
│   └── agents/                ← 5 AI agents
│       ├── planner.md
│       ├── executor.md
│       ├── context-finder.md
│       ├── researcher.md
│       └── document.md        ← NEW
└── .ccc/
    ├── templates/             ← document templates
    │   └── govdoc/            ← Thai gov docs
    ├── docs/                  ← generated documents
    └── memory/
        ├── retrospectives/
        └── learnings/
```

**When to use:** Most projects. You get the workflow commands and storage for retrospectives.

**Output:**
```
✅ CCC Workflow installed!

Commands (12): .claude/commands/
  Core:      ccc, nnn, gogogo, lll
  Context:   rrr, wip, recap, forward
  Research:  research, review
  Document:  template, mcp-setup

Agents (5): .claude/agents/
  planner, executor, context-finder, researcher, document

Directories: .ccc/
  memory/     (retrospectives, learnings)
  templates/  (document templates)
  docs/       (generated documents)

Ready! Try: /nnn "your first task"
```

---

### Option 2: `/awaken --full` (With Project Docs)

```bash
/awaken --full
```

**What it creates:**

```
your-project/
├── .claude/
│   ├── commands/              ← Same as standard
│   └── agents/                ← Same as standard
└── .ccc/
    ├── HOME.md                ← Project overview & quick start
    ├── WIP.md                 ← Current work in progress tracker
    ├── DECISIONS.md           ← Architecture decision records
    └── memory/
        ├── retrospectives/
        └── learnings/
```

**The extra files:**

#### `HOME.md` - Project Overview
```markdown
# Project Home

## Overview
[Brief description of this project]

## Quick Start
/lll          # See status
/nnn "task"   # Plan something
/gogogo       # Execute plan

## Architecture
[Key technical decisions]

## Links
- Repo: [url]
- Docs: [url]
```

#### `WIP.md` - Work In Progress
```markdown
# Work In Progress

## Current Focus
[What's being worked on now]

## Recent
- [Recent item 1]
- [Recent item 2]

## Blocked
[Any blockers]
```

#### `DECISIONS.md` - Architecture Decisions
```markdown
# Architecture Decisions

## Template
### [Decision Title]
**Date**: YYYY-MM-DD
**Status**: [Proposed | Accepted | Deprecated]

**Context**: Why this decision was needed
**Decision**: What was decided
**Consequences**: What this means
```

**When to use:**
- New projects where you want structured documentation
- Team projects where you need to track decisions
- Long-running projects that benefit from a "home base"

**Output:**
```
✅ CCC Workflow installed!

Commands (10): .claude/commands/
Agents (4): .claude/agents/

Project docs: .ccc/
  HOME.md, WIP.md, DECISIONS.md
  memory/retrospectives/, memory/learnings/

Ready! Try: /nnn "your first task"
```

---

### Option 3: `/awaken --dir <name>` (Custom Directory)

```bash
/awaken --dir .soul
```

**What it creates:**

```
your-project/
├── .claude/
│   ├── commands/              ← Always in .claude/
│   └── agents/                ← Always in .claude/
└── .soul/                     ← YOUR CUSTOM NAME
    └── memory/
        ├── retrospectives/
        └── learnings/
```

**Examples:**
```bash
/awaken --dir .soul      # Creates .soul/memory/
/awaken --dir .ai        # Creates .ai/memory/
/awaken --dir memory     # Creates memory/memory/ (not recommended)
/awaken --dir project    # Creates project/memory/
```

**Combine with --full:**
```bash
/awaken --full --dir .soul
```

Creates:
```
.soul/
├── HOME.md
├── WIP.md
├── DECISIONS.md
└── memory/
    ├── retrospectives/
    └── learnings/
```

**When to use:**
- You prefer a different directory name
- Following a convention from another project (like `ψ` from nat-agents)
- Avoiding conflicts with existing `.ccc` directory

---

## Comparison Table

| Feature | `/awaken` | `/awaken --full` | `/awaken --dir X` |
|---------|-----------|------------------|-------------------|
| Commands in `.claude/commands/` | ✓ | ✓ | ✓ |
| Agents in `.claude/agents/` | ✓ | ✓ | ✓ |
| `memory/retrospectives/` | ✓ | ✓ | ✓ |
| `memory/learnings/` | ✓ | ✓ | ✓ |
| `HOME.md` | - | ✓ | with --full |
| `WIP.md` | - | ✓ | with --full |
| `DECISIONS.md` | - | ✓ | with --full |
| Directory name | `.ccc` | `.ccc` | Custom |

---

## After `/awaken` - The Workflow

### Daily Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `/nnn "task"` | Plan a task | `/nnn "Add dark mode"` |
| `/gogogo` | Execute latest plan | `/gogogo` |
| `/lll` | See project status | `/lll` |

### Context Commands (Optional)

| Command | Purpose | When to Use |
|---------|---------|-------------|
| `/ccc` | Save context to GitHub | Before breaks, switching tasks |
| `/recap` | Get session summary | Starting a new session |
| `/wip` | Show current work | Check what's in progress |
| `/forward` | Forward context | Before `/clear` |
| `/rrr` | Write retrospective | After completing work |

### Research Commands (New!)

| Command | Purpose | Example |
|---------|---------|---------|
| `/research <url>` | Analyze website/docs | `/research https://nextjs.org/docs` |
| `/research github:user/repo` | Analyze GitHub repo | `/research github:facebook/react` |
| `/research "query"` | Search and research | `/research "React Server Components"` |
| `/review` | Review current project | `/review` |
| `/review security` | Security-focused review | `/review security` |
| `/review github:user/repo` | Review external repo | `/review github:shadcn/ui` |

---

## Example: Complete Project Setup

### New React Project

```bash
# Create project
npx create-next-app my-app
cd my-app

# Setup CCC workflow
/awaken --full

# Start working
/nnn "Add user authentication with NextAuth"
/gogogo
```

### Existing Project (Minimal)

```bash
cd existing-project

# Just the basics
/awaken

# Start working
/nnn "Fix bug #42"
/gogogo
```

### Team Project with Custom Directory

```bash
cd team-project

# Full setup with custom dir
/awaken --full --dir .project

# Now you have:
# .project/HOME.md      - Team reads this first
# .project/WIP.md       - Track who's doing what
# .project/DECISIONS.md - Record architecture choices
```

---

## Workflow Examples

### Simple Feature

```bash
/nnn "Add export to CSV button"
/gogogo
# Done! PR ready for review
```

### Bug Fix

```bash
/nnn "#123"              # Reference existing issue
/gogogo
```

### Multi-Day Feature

```bash
# Day 1
/nnn "Build payment integration"
/gogogo                   # Partial progress
/ccc                      # Save context

# Day 2
/recap                    # Catch up on context
/gogogo                   # Continue work
/rrr                      # Write retrospective
```

### Check Status Anytime

```bash
/lll
```

Output:
```
## Project Status

Branch: main (clean)

Open Issues (3):
  #5 - plan: Add payments
  #4 - bug: Login timeout
  #2 - context: Yesterday's work

Open PRs (1):
  #6 - feat: Add CSV export

Recent Commits:
  abc123 feat: CSV export button
  def456 fix: Validation error
```

---

## The Agents

`/awaken` installs 4 specialized AI agents:

| Agent | Model | Purpose | Used By |
|-------|-------|---------|---------|
| `planner` | Sonnet | Research codebase, create plans | `/nnn` |
| `executor` | Sonnet | Execute plans safely | `/gogogo` |
| `context-finder` | Haiku | Fast codebase search | Internal |
| `researcher` | Sonnet | Research web, GitHub, papers | `/research`, `/review` |

**Security:** Each agent has restricted tools:
- `planner` - Read-only (can't modify files)
- `executor` - No force flags, no auto-merge
- `context-finder` - Read-only, fast
- `researcher` - Read-only, web access, temp clones only

---

## Tips

### Do
- Run `/awaken` once when starting on a project
- Use `/nnn` before writing code
- Run `/lll` to check status
- Use `/ccc` before taking breaks

### Don't
- Run `/awaken` multiple times (it's idempotent, but unnecessary)
- Skip `/nnn` and code directly (plans help!)
- Forget to `/ccc` before long breaks

---

## Research & Review Examples

### Research a GitHub Repository

```bash
/research github:shadcn/ui
```

**Output:**
```markdown
## Repository Analysis: shadcn/ui

**Stars**: 50k+ | **Language**: TypeScript
**License**: MIT | **Updated**: Recently

### Overview
Beautifully designed components built with Radix UI and Tailwind CSS.

### Project Structure
- apps/www/ - Documentation site
- packages/cli/ - CLI tool
- packages/ui/ - Component source

### Key Patterns
- Radix UI primitives for accessibility
- Tailwind CSS for styling
- cn() utility for class merging

### Learning Path
1. Start with components/ui/button.tsx
2. Study the cn() utility
3. Look at Radix UI integration
```

### Research Documentation

```bash
/research https://nextjs.org/docs/app/building-your-application/routing
```

**Output:**
```markdown
## Website Analysis: Next.js App Router

### Key Concepts
- File-based routing
- Layouts and templates
- Loading and error states
- Parallel and intercepting routes

### Important Sections
- Route Groups - Organize without affecting URL
- Dynamic Routes - [slug] pattern
- Route Handlers - API endpoints
```

### Review Current Project

```bash
/review
```

**Output:**
```markdown
## Project Review: my-app

### Health Score: 8/10

### Strengths
✓ TypeScript strict mode
✓ Good test coverage (75%)
✓ Clean architecture

### Areas for Improvement
⚠ 3 TODO comments unaddressed
⚠ Missing error boundaries
⚠ 2 unused dependencies

### Recommendations
1. Add error boundaries
2. Remove unused: moment, lodash
3. Address TODOs in src/utils/
```

---

## Real World Example: E-Commerce Project

Complete walkthrough from setup to shipping features.

### Day 0: Project Setup

```bash
# You just cloned a Next.js e-commerce project
git clone https://github.com/company/shop-app
cd shop-app

# Install CCC workflow
/awaken --full
```

**Output:**
```
✅ CCC Workflow installed!

Commands (8): .claude/commands/
Agents (3): .claude/agents/
Project docs: .ccc/
  HOME.md, WIP.md, DECISIONS.md
  memory/retrospectives/, memory/learnings/

Ready! Try: /nnn "your first task"
```

**Your project now:**
```
shop-app/
├── .claude/
│   ├── commands/        ← Your workflow tools
│   └── agents/          ← AI helpers
├── .ccc/
│   ├── HOME.md          ← Fill in project overview
│   ├── WIP.md           ← Track current work
│   ├── DECISIONS.md     ← Record decisions
│   └── memory/
├── src/
├── package.json
└── ...
```

---

### Day 1: First Feature - Add to Cart

```bash
# Check what's happening
/lll
```

**Output:**
```
## Project Status

Branch: main (clean)

Open Issues (1):
  #12 - feat: Add to cart functionality

Open PRs (0)
No open PRs

Recent Commits:
  a1b2c3d Initial commit
  d4e5f6g Setup Next.js with Tailwind
```

```bash
# Plan the feature
/nnn "Implement add to cart for issue #12"
```

**What happens:**
1. Planner agent searches your codebase
2. Finds: `src/components/ProductCard.tsx`, `src/store/`, `src/types/`
3. Creates detailed plan issue

**Output:**
```
✅ Plan created: #13
   "plan: Implement add to cart functionality"

Research found:
  - src/components/ProductCard.tsx (needs cart button)
  - src/store/index.ts (Zustand store exists)
  - src/types/product.ts (Product type defined)
  - No cart state exists yet

Ready to /gogogo
```

**GitHub Issue #13 created:**
```markdown
# Implementation Plan: Add to Cart

**Created**: 2024-01-15 10:30 GMT+7

## Problem Statement
Add "Add to Cart" functionality to product cards.

## Research Summary
### Relevant Files
- `src/components/ProductCard.tsx` - Add button here
- `src/store/index.ts` - Zustand store, add cart slice
- `src/types/product.ts` - Product type exists

### Existing Patterns
- Using Zustand for state management
- Tailwind for styling
- Product type: { id, name, price, image }

## Implementation Steps

### Phase 1: Cart State
- [ ] Create cart types (CartItem, CartState)
- [ ] Add cart slice to Zustand store
- [ ] Implement addToCart, removeFromCart, clearCart

### Phase 2: UI Components
- [ ] Create AddToCartButton component
- [ ] Add button to ProductCard
- [ ] Create CartIcon with item count badge

### Phase 3: Cart Drawer
- [ ] Create CartDrawer component
- [ ] Show cart items with quantities
- [ ] Add remove and quantity controls

## Success Criteria
- [ ] Can add products to cart
- [ ] Cart persists across page navigation
- [ ] Cart icon shows item count
- [ ] Can view and modify cart contents
```

```bash
# Execute the plan
/gogogo
```

**Output (during execution):**
```
📋 Executing Plan #13: "Add to Cart"

[1/7] Creating cart types...
      → Creating src/types/cart.ts
      ✓ Done

[2/7] Adding cart slice to store...
      → Modifying src/store/index.ts
      ✓ Done

[3/7] Implementing cart actions...
      → addToCart, removeFromCart, updateQuantity, clearCart
      ✓ Done

[4/7] Creating AddToCartButton component...
      → Creating src/components/AddToCartButton.tsx
      ✓ Done

[5/7] Adding button to ProductCard...
      → Modifying src/components/ProductCard.tsx
      ✓ Done

[6/7] Creating CartIcon component...
      → Creating src/components/CartIcon.tsx
      ✓ Done

[7/7] Creating CartDrawer component...
      → Creating src/components/CartDrawer.tsx
      ✓ Done

Running build... ✓ Passed
Running tests... ✓ 8 passed

Creating commit and PR...
```

**Final output:**
```
✅ Plan #13 executed!

Created:
  + src/types/cart.ts
  + src/components/AddToCartButton.tsx
  + src/components/CartIcon.tsx
  + src/components/CartDrawer.tsx

Modified:
  ~ src/store/index.ts
  ~ src/components/ProductCard.tsx
  ~ src/app/layout.tsx

Build: ✓ Passed
Tests: ✓ 8 passed

Branch: feat/13-add-to-cart
Commit: abc1234
PR: #14 (ready for review)

Plan #13 closed.
```

```bash
# End of day - save context
/ccc
```

**Output:**
```
✅ Context saved: #15
   "context: Add to cart complete, PR #14 ready"
```

---

### Day 2: Code Review Feedback

Your teammate reviewed PR #14 and left comments. Start new session:

```bash
# What's the status?
/lll
```

**Output:**
```
## Project Status

Branch: feat/13-add-to-cart

Open Issues (2):
  #15 - context: Add to cart complete
  #12 - feat: Add to cart functionality

Open PRs (1):
  #14 - feat: Add to cart [Changes requested]

Recent Commits:
  abc1234 feat: Add to cart functionality
```

```bash
# Get context from yesterday
/recap
```

**Output:**
```
## Session Recap

### Current State
- Branch: feat/13-add-to-cart
- PR #14 has review comments
- Feature mostly complete

### Review Feedback (from PR #14)
- Add loading state to AddToCartButton
- Handle out-of-stock products
- Add toast notification on add

### Suggested Next Steps
1. Address review comments
2. Push updates to PR #14
```

```bash
# Plan the fixes
/nnn "Address PR #14 review feedback"
```

**Output:**
```
✅ Plan created: #16
   "plan: Address PR review feedback"

Steps:
  1. Add loading state to AddToCartButton
  2. Add stock check before adding
  3. Add toast notification

Ready to /gogogo
```

```bash
/gogogo
# Makes changes, pushes to same branch
# PR #14 auto-updates
```

---

### Day 3: New Feature - Wishlist

PR #14 merged! Start new feature:

```bash
/lll
```

**Output:**
```
## Project Status

Branch: main (+1 ahead after merge)

Open Issues (1):
  #18 - feat: Add wishlist functionality

Open PRs (0)
All merged!

Recent Commits:
  xyz789 feat: Add to cart (#14)
```

```bash
# Plan next feature
/nnn "#18"   # Reference existing issue
```

```bash
/gogogo
```

```bash
# End of week - write retrospective
/rrr
```

**Creates:** `.ccc/memory/retrospectives/2024-01-17_retrospective.md`

---

### Weekly Summary

```bash
/lll
```

**Output:**
```
## Project Status

Branch: main (clean)

Open Issues (2):
  #22 - feat: Checkout flow
  #21 - context: Week 1 complete

Open PRs (0)
All merged!

Recent Commits (this week):
  def456 feat: Wishlist functionality (#19)
  xyz789 feat: Add to cart (#14)

Stats:
  - 2 features shipped
  - 3 PRs merged
  - 0 bugs introduced
```

---

### Quick Reference for This Project

```bash
# Morning routine
/lll                    # What's the status?
/recap                  # What was I doing?

# Working on features
/nnn "description"      # Plan it
/nnn "#42"              # Plan from issue
/gogogo                 # Build it

# Before breaks
/ccc                    # Save context

# End of day/week
/rrr                    # Retrospective
```

---

## Step-by-Step: Document Generation Project

Complete guide for building a document generation system (e.g., Thai government documents).

### Phase 1: Setup (Day 1)

```bash
# Create your project
mkdir thai-govdoc-ai
cd thai-govdoc-ai
git init

# Setup CCC workflow with full templates
/awaken --full
```

**Your project now has:**
```
thai-govdoc-ai/
├── .claude/
│   ├── commands/      ← 12 commands ready
│   └── agents/        ← 5 agents ready
└── .ccc/
    ├── HOME.md        ← Edit with project info
    ├── templates/
    │   └── govdoc/    ← Thai document templates
    └── docs/          ← Generated documents go here
```

### Phase 2: Setup MCP for Word/PDF (Day 1)

```bash
# View MCP setup guide
/mcp-setup documents
```

**Add to `~/.claude/settings.json`:**
```json
{
  "mcpServers": {
    "document-operations": {
      "command": "uvx",
      "args": ["document-operations-mcp"]
    }
  }
}
```

**Restart Claude Code and verify:**
```bash
exit
claude
/mcp
```

### Phase 3: Research (Day 1-2)

```bash
# Research Thai government document formats
/research "หนังสือราชการ format ระเบียบสำนักนายกรัฐมนตรี"

# Research existing tools
/research github:whs/typst-govdoc

# Download official templates
/research https://www.kruchiangrai.net/2021/11/12/หนังสือราชการ/
```

### Phase 4: Plan Your System (Day 2)

```bash
# Create implementation plan
/nnn "Build Thai government document generator with AI"
```

**Plan will include:**
- Document understanding agent
- Template selection logic
- Content generation with formal Thai
- Format validation
- Word/PDF output

### Phase 5: Implement (Day 3-5)

```bash
# Execute the plan
/gogogo

# Review implementation
/review
```

### Phase 6: Use Templates (Ongoing)

```bash
# List available templates
/template list

# Create memo
/template create govdoc-memo "ขอความอนุเคราะห์ข้อมูล"

# Create external letter
/template create govdoc-external "ขอเชิญเป็นวิทยากร"
```

### Complete Workflow

```
/awaken --full          # Setup project
        ↓
/mcp-setup documents    # Setup Word/PDF MCP
        ↓
/research               # Research requirements
        ↓
/nnn "your system"      # Plan implementation
        ↓
/gogogo                 # Build it
        ↓
/template create        # Use templates
        ↓
MCP converts to Word/PDF
        ↓
Final Document Ready!
```

### Document Commands Reference

| Command | Purpose |
|---------|---------|
| `/template list` | Show all templates |
| `/template get <name>` | Download template |
| `/template create <name> "title"` | Create document |
| `/mcp-setup documents` | Setup MCP for docs |

### Thai Government Document Templates

| Template | Thai Name |
|----------|-----------|
| `govdoc-external` | หนังสือภายนอก |
| `govdoc-internal` | หนังสือภายใน |
| `govdoc-memo` | บันทึกข้อความ |
| `govdoc-order` | คำสั่ง |
| `govdoc-announce` | ประกาศ |

---

## Troubleshooting

### "Command not found"

```bash
# Make sure plugin is installed
/install-plugin github:dearxcorex/plugin-claude

# Then run awaken
/awaken
```

### "Already have .claude/ directory"

`/awaken` will add to existing `.claude/` without overwriting your settings.

### "Want to reset"

```bash
# Remove and reinstall
rm -rf .claude/commands .claude/agents .ccc
/awaken
```

---

## License

MIT

## Author

[@dearxcorex](https://github.com/dearxcorex)
