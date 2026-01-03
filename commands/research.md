---
description: Research websites, GitHub repos, and papers
allowed-tools:
  - WebFetch
  - WebSearch
  - Read
  - Bash
  - Task
  - Glob
  - Grep
---

# Research - Deep Dive into External Resources

Research and analyze websites, GitHub repositories, and papers.

## Usage

```bash
# Research a website
/research https://nextjs.org/docs/app

# Research a GitHub repo
/research github:vercel/next.js

# Research a paper/article
/research paper:https://arxiv.org/abs/2304.xxxxx

# Search and research
/research "React Server Components best practices"
```

## How It Works

```
/research <target>
  │
  ├─→ Detect type (URL, GitHub, Paper, Search query)
  │
  ├─→ Spawn researcher agent
  │
  ├─→ Fetch and analyze content
  │
  └─→ Return structured summary
```

## Research Types

### 1. Website/Documentation

```bash
/research https://docs.python.org/3/library/asyncio.html
```

**Process:**
1. Fetch URL with WebFetch
2. Extract main content
3. Identify key concepts
4. Summarize with structure

**Output:**
```markdown
## Website Analysis: Python asyncio Documentation

### Overview
Official Python documentation for asyncio - asynchronous I/O framework.

### Key Concepts
- Event loops
- Coroutines and Tasks
- Streams
- Synchronization primitives

### Important Sections
- [Coroutines](url) - Foundation of async/await
- [Tasks](url) - Running coroutines concurrently
- [Streams](url) - Network I/O

### Quick Summary
asyncio provides infrastructure for writing single-threaded concurrent
code using coroutines, multiplexing I/O access over sockets, and more.
```

---

### 2. GitHub Repository

```bash
/research github:facebook/react
```

**Process:**
1. Fetch repo info via GitHub API (WebFetch)
2. Clone to temp directory (Bash)
3. Analyze structure (Glob, Grep)
4. Identify patterns and key files

**Output:**
```markdown
## Repository Analysis: facebook/react

**Stars**: 220k | **Forks**: 45k | **Language**: JavaScript
**License**: MIT | **Last Updated**: 2 days ago

### Overview
A declarative, efficient, and flexible JavaScript library for building
user interfaces.

### Project Structure
```
react/
├── packages/           # Monorepo packages
│   ├── react/          # Core React package
│   ├── react-dom/      # DOM-specific methods
│   └── react-reconciler/  # Reconciliation algorithm
├── scripts/            # Build and test scripts
└── fixtures/           # Test fixtures
```

### Tech Stack
- Build: Rollup, Babel
- Testing: Jest
- Type checking: Flow
- Package manager: Yarn (workspaces)

### Key Patterns
- **Fiber Architecture**: Incremental rendering
- **Hooks**: State and lifecycle in functions
- **Reconciliation**: Efficient DOM updates

### Notable Files to Study
| File | Why |
|------|-----|
| `packages/react/src/React.js` | Entry point |
| `packages/react/src/ReactHooks.js` | Hooks implementation |
| `packages/react-reconciler/src/ReactFiberReconciler.js` | Core algorithm |

### Learning Path
1. Start with `packages/react/src/React.js`
2. Understand hooks in `ReactHooks.js`
3. Study the reconciler for deep understanding
4. Look at `react-dom` for DOM specifics

### Insights for Your Project
- Consider monorepo structure for large projects
- Hooks pattern is highly reusable
- Fiber architecture enables concurrent features
```

---

### 3. Paper/Article

```bash
/research paper:https://arxiv.org/abs/2304.03442
```

**Process:**
1. Fetch paper content (WebFetch)
2. Extract abstract, sections
3. Identify key contributions
4. Summarize methodology and results

**Output:**
```markdown
## Paper Summary: [Title]

**Authors**: Author 1, Author 2, et al.
**Published**: Conference/Journal, Year
**Link**: [arxiv](url)

### TL;DR
One sentence summary of the paper's main contribution.

### Abstract
[Shortened abstract]

### Key Contributions
1. Novel approach to X
2. Improved performance on Y
3. New dataset for Z

### Methodology
- Step 1: Data collection
- Step 2: Model architecture
- Step 3: Training procedure

### Results
| Metric | Theirs | Previous SOTA |
|--------|--------|---------------|
| Accuracy | 95% | 92% |

### Relevance to Your Work
- Technique X could be applied to your project
- Dataset Y might be useful for testing
```

---

### 4. Search Query

```bash
/research "Next.js 14 server actions best practices"
```

**Process:**
1. WebSearch for relevant results
2. Fetch top 3-5 results
3. Synthesize information
4. Provide comprehensive answer

**Output:**
```markdown
## Research: Next.js 14 Server Actions Best Practices

### Summary
Server Actions in Next.js 14 allow server-side mutations without API routes...

### Best Practices Found

1. **Form Handling**
   - Use `useFormStatus` for loading states
   - Validate on server with Zod
   - Source: [Next.js Docs](url)

2. **Error Handling**
   - Return error objects, don't throw
   - Use `useFormState` for error display
   - Source: [Blog Post](url)

3. **Revalidation**
   - Call `revalidatePath()` after mutations
   - Use `revalidateTag()` for granular control
   - Source: [Vercel Guide](url)

### Code Examples
```typescript
'use server'

export async function createPost(formData: FormData) {
  const validated = schema.safeParse(...)
  if (!validated.success) {
    return { error: validated.error.message }
  }

  await db.post.create(...)
  revalidatePath('/posts')
  return { success: true }
}
```

### Sources
- [Next.js Documentation](url)
- [Vercel Blog](url)
- [Community Guide](url)
```

## Spawning Researcher Agent

For complex research, spawn the researcher agent:

```
Task tool:
  subagent_type: "researcher"
  model: sonnet
  prompt: |
    Research [target]

    Focus on:
    - [specific aspect 1]
    - [specific aspect 2]

    Output format: [website|github|paper]
```

## Tips

| Do | Don't |
|----|-------|
| Be specific about what you want | Vague queries like "research React" |
| Ask for specific aspects | Ask to research entire ecosystems |
| Use for learning & understanding | Use for copying code |

## Examples

```bash
# Learn from a well-structured project
/research github:shadcn/ui

# Understand a new API
/research https://platform.openai.com/docs/api-reference

# Study an algorithm paper
/research paper:https://arxiv.org/abs/1706.03762

# Find best practices
/research "TypeScript monorepo setup 2024"
```
