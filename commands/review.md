---
description: Review and analyze projects
allowed-tools:
  - Read
  - Glob
  - Grep
  - Bash
  - Task
  - WebFetch
---

# Review - Project Analysis & Health Check

Analyze projects for quality, patterns, security, and improvements.

## Usage

```bash
# Review current project
/review

# Review specific area
/review security
/review performance
/review architecture

# Review external GitHub repo
/review github:user/repo
```

## How It Works

```
/review
  │
  ├─→ Scan project structure
  │
  ├─→ Analyze code patterns
  │
  ├─→ Check for issues
  │
  └─→ Generate report with score
```

## Review Types

### 1. Full Review (Default)

```bash
/review
```

**Checks:**
- Project structure
- Code quality
- Test coverage
- Security issues
- Dependencies
- Documentation

**Output:**
```markdown
## Project Review: my-app

### Health Score: 8.5/10

### Overview
| Metric | Value |
|--------|-------|
| Files | 156 |
| Lines of Code | 12,450 |
| Languages | TypeScript, CSS |
| Test Files | 23 |

---

### ✅ Strengths

**Code Quality**
- TypeScript with strict mode enabled
- Consistent code style (ESLint + Prettier)
- Good component organization

**Testing**
- Test coverage: 78%
- Unit tests for utilities
- Integration tests for API

**Structure**
- Clean folder organization
- Separation of concerns
- Reusable components

---

### ⚠️ Areas for Improvement

**Missing Error Boundaries**
- Location: `src/app/`
- Impact: Unhandled errors crash entire app
- Suggestion: Add ErrorBoundary wrapper

**TODO Comments (5 found)**
```
src/utils/api.ts:45    // TODO: Add retry logic
src/hooks/useAuth.ts:12  // TODO: Handle token refresh
...
```

**Large Components**
| File | Lines | Suggestion |
|------|-------|------------|
| `src/components/Dashboard.tsx` | 450 | Split into smaller components |
| `src/pages/Settings.tsx` | 380 | Extract settings sections |

---

### 🔒 Security

**Status**: ⚠️ Minor Issues

| Check | Status |
|-------|--------|
| No secrets in code | ✅ Pass |
| Dependencies up to date | ⚠️ 3 outdated |
| Known vulnerabilities | ⚠️ 2 low severity |
| Env file in gitignore | ✅ Pass |

**Recommended Actions:**
```bash
npm audit fix
npm update lodash axios
```

---

### 📦 Dependencies

**Total**: 45 packages (12 dev)

**Outdated:**
| Package | Current | Latest |
|---------|---------|--------|
| axios | 1.4.0 | 1.6.0 |
| lodash | 4.17.20 | 4.17.21 |

**Unused (detected):**
- `moment` - Consider removing

---

### 📝 Documentation

| Item | Status |
|------|--------|
| README.md | ✅ Exists |
| API docs | ❌ Missing |
| Component docs | ⚠️ Partial |
| Contributing guide | ❌ Missing |

---

### 🎯 Recommendations

**High Priority**
1. Add error boundaries to prevent crashes
2. Fix 2 security vulnerabilities with `npm audit fix`

**Medium Priority**
3. Split large components (Dashboard, Settings)
4. Add API documentation
5. Address TODO comments

**Low Priority**
6. Remove unused `moment` dependency
7. Add contributing guide

---

### Quick Fixes

```bash
# Fix vulnerabilities
npm audit fix

# Update outdated packages
npm update axios lodash

# Remove unused package
npm uninstall moment
```
```

---

### 2. Security Review

```bash
/review security
```

**Checks:**
- Secrets in code
- Environment files
- Dependencies vulnerabilities
- Auth patterns
- Input validation
- SQL/XSS patterns

**Output:**
```markdown
## Security Review: my-app

### Overall: ⚠️ Needs Attention

---

### 🔑 Secrets Scan

| Check | Status | Details |
|-------|--------|---------|
| API keys in code | ✅ Pass | No hardcoded keys found |
| .env in .gitignore | ✅ Pass | Properly ignored |
| Sensitive files | ✅ Pass | No credentials files |

---

### 📦 Dependency Vulnerabilities

```bash
npm audit
```

| Severity | Count |
|----------|-------|
| Critical | 0 |
| High | 0 |
| Moderate | 2 |
| Low | 1 |

**Details:**
| Package | Severity | Issue | Fix |
|---------|----------|-------|-----|
| nth-check | Moderate | ReDoS | Update css-select |
| semver | Low | ReDoS | Update to 7.5.4 |

---

### 🔐 Auth Patterns

| Check | Status |
|-------|--------|
| Password hashing | ✅ bcrypt used |
| JWT verification | ✅ Proper validation |
| Session handling | ⚠️ No refresh token |

**Recommendation:** Implement token refresh for better security.

---

### 🛡️ Input Validation

| Area | Status |
|------|--------|
| Form inputs | ✅ Zod validation |
| API endpoints | ⚠️ 2 missing validation |
| File uploads | ✅ Type checking |

**Missing validation:**
- `src/app/api/users/route.ts:23`
- `src/app/api/posts/route.ts:45`

---

### 🚫 Dangerous Patterns

| Pattern | Found | Location |
|---------|-------|----------|
| eval() | ❌ None | - |
| dangerouslySetInnerHTML | ⚠️ 1 | `src/components/RichText.tsx:12` |
| SQL concatenation | ❌ None | - |

---

### Recommendations

1. **Fix npm vulnerabilities**
   ```bash
   npm audit fix
   ```

2. **Add validation to API endpoints**
   - `src/app/api/users/route.ts`
   - `src/app/api/posts/route.ts`

3. **Review dangerouslySetInnerHTML usage**
   - Ensure input is sanitized with DOMPurify
```

---

### 3. Architecture Review

```bash
/review architecture
```

**Output:**
```markdown
## Architecture Review: my-app

### Pattern: Next.js App Router + Feature-Based Structure

---

### Project Structure

```
src/
├── app/                 # Routes (App Router)
│   ├── (auth)/          # Auth group
│   ├── (dashboard)/     # Dashboard group
│   └── api/             # API routes
├── components/
│   ├── ui/              # Base UI components
│   └── features/        # Feature components
├── lib/                 # Utilities
├── hooks/               # Custom hooks
├── store/               # State management
└── types/               # TypeScript types
```

### Assessment: ✅ Well Organized

---

### Patterns Identified

| Pattern | Usage | Assessment |
|---------|-------|------------|
| Route Groups | `(auth)`, `(dashboard)` | ✅ Good |
| Server Components | Default | ✅ Good |
| Client Components | `'use client'` where needed | ✅ Good |
| API Routes | `app/api/*` | ✅ Good |
| State Management | Zustand | ✅ Good |

---

### Component Architecture

**Composition Pattern**: ✅ Used correctly
```tsx
<Card>
  <Card.Header />
  <Card.Body />
  <Card.Footer />
</Card>
```

**Custom Hooks**: ✅ Well abstracted
- `useAuth()` - Auth state
- `useTasks()` - Task CRUD
- `useDebounce()` - Input debouncing

---

### Data Flow

```
User Action
    ↓
Client Component (useFormStatus)
    ↓
Server Action
    ↓
Database (Prisma)
    ↓
Revalidation
    ↓
Updated UI
```

**Assessment**: ✅ Clean unidirectional flow

---

### Suggestions

1. **Consider adding:**
   - Error boundary at route level
   - Suspense boundaries for loading states
   - Parallel routes for modals

2. **Could improve:**
   - Move shared types to `@/types`
   - Add barrel exports in feature folders
```

---

### 4. External Repo Review

```bash
/review github:shadcn/ui
```

**Process:**
1. Fetch repo info
2. Clone to temp
3. Analyze structure
4. Generate insights

**Output:**
```markdown
## External Review: shadcn/ui

**Stars**: 50k+ | **License**: MIT

### What We Can Learn

**Component Architecture**
- Uses Radix UI primitives
- Tailwind for styling
- cn() utility for class merging

**Code Patterns Worth Adopting**
1. Component composition pattern
2. Variant system with cva()
3. Theme with CSS variables

**File Structure**
```
components/
└── ui/
    ├── button.tsx      # Self-contained
    ├── card.tsx        # With sub-components
    └── dialog.tsx      # Radix wrapper
```

### Applicable to Your Project
- [ ] Adopt cn() utility
- [ ] Use cva() for button variants
- [ ] Consider CSS variables for theming
```

## Quick Commands

```bash
/review                    # Full review
/review security           # Security focus
/review architecture       # Structure focus
/review performance        # Performance focus
/review github:user/repo   # External repo
```
