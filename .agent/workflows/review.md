---
description: Five-axis code review. Structured quality gate for correctness, readability, architecture, security, and performance.
---

# /review - Structured Code Review

$ARGUMENTS

---

## 🔴 CRITICAL RULES

1. **READ before judging** — Understand context and intent first
2. **5 axes review** — Every review must cover all 5 axes
3. **Surgical feedback** — File:line references, not vague suggestions
4. **Categorize findings** — Critical / Important / Suggestion
5. **No drive-by fixes** — Report issues, don't silently fix unrelated code

---

## Task

### Step 1: Identify Scope

Determine what to review:
- If `$ARGUMENTS` specifies files → review those files
- If no arguments → review recent changes (git diff or recently edited files)
- If "all" → review entire codebase (warn about token cost first)

### Step 2: Five-Axis Review

For each file/change, evaluate all 5 axes:

#### ✅ Axis 1: Correctness
- Does it match the spec/requirements?
- Are edge cases handled?
- Are tests adequate and passing?
- Could it fail silently?
- Are error messages helpful for debugging?

#### 📖 Axis 2: Readability
- Clear variable and function names?
- Straightforward logic flow?
- Well-organized structure?
- Would a new team member understand it in 5 minutes?
- Comments explain WHY, not WHAT?

#### 🏗️ Axis 3: Architecture
- Follows existing patterns in the codebase?
- Clean module boundaries?
- Right level of abstraction? (not over-engineered, not under-engineered)
- Dependencies pointing the right direction?
- Single Responsibility Principle respected?

#### 🔒 Axis 4: Security
- Input validated and sanitized?
- No secrets or API keys in code?
- Authentication/authorization checked on all sensitive paths?
- SQL injection / XSS risks?
- Load `vulnerability-scanner` skill if issues found

#### ⚡ Axis 5: Performance
- No N+1 queries?
- No unbounded operations on large datasets?
- Assets and images optimized?
- Unnecessary re-renders in UI code?
- Load `performance-profiling` skill if issues found

### Step 3: Output Report

Format findings as:

```markdown
## 🔍 Code Review: [Scope]

### Critical ❌ (Must fix before merge)
| # | File:Line | Issue | Suggested Fix |
|---|-----------|-------|---------------|
| 1 | `src/auth.ts:42` | SQL injection via string concat | Use parameterized query |

### Important ⚠️ (Should fix)
| # | File:Line | Issue | Suggested Fix |
|---|-----------|-------|---------------|

### Suggestions 💡 (Nice to have)
| # | File:Line | Issue | Suggested Fix |
|---|-----------|-------|---------------|

### ✅ What's Good
- [Specific positive observations]

### Scorecard
| Axis | Rating | Notes |
|------|--------|-------|
| Correctness | ✅/⚠️/❌ | |
| Readability | ✅/⚠️/❌ | |
| Architecture | ✅/⚠️/❌ | |
| Security | ✅/⚠️/❌ | |
| Performance | ✅/⚠️/❌ | |
```

---

## Agent Routing

- Security issues found → Load `security-auditor` agent
- Performance issues found → Load `performance-optimizer` agent
- Architecture concerns → Load `backend-specialist` or `frontend-specialist`

---

## Anti-Rationalization

| Excuse | Rebuttal |
|--------|----------|
| "Code looks fine, no issues" | There are ALWAYS findings. Look harder at all 5 axes. |
| "Too simple to review" | Simple code = fast review. Still review all 5 axes. |
| "I wrote this code, it's correct" | Author bias is real. Review objectively. |
| "Only cosmetic issues" | Readability IS a valid axis. Report them as Suggestions. |
| "Security is overkill for this" | EVERY code path touching user data needs security review. |

---

## Usage

```
/review
/review src/services/auth.ts
/review src/components/
/review all
/review recent changes
```
