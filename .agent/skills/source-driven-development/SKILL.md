---
name: source-driven-development
description: Grounds implementation decisions in official documentation. Use when building with any framework where correctness matters. Prevents outdated patterns from training data.
version: 1.0
priority: HIGH
---

# Source-Driven Development

> Don't code from memory — verify, cite, and let the user see your sources.

---

## When to Use

- Building with framework-specific patterns (forms, routing, data fetching, auth)
- Creating boilerplate or starter code that will be copied across a project
- User asks for "correct", "verified", or "best practice" implementation
- Any time you're about to write framework-specific code from memory

**When NOT to use:**
- Pure logic (loops, conditionals, data structures)
- Renaming variables, fixing typos, moving files
- User explicitly wants speed over verification

---

## The Process

```
DETECT ──→ FETCH ──→ IMPLEMENT ──→ CITE
  │          │           │            │
  ▼          ▼           ▼            ▼
 What       Get the    Follow the   Show your
 stack?     relevant   documented   sources
            docs       patterns
```

### Step 1: Detect Stack and Versions

Read the project's dependency file to identify exact versions:

```
package.json    → Node/React/Vue/Angular
composer.json   → PHP/Laravel
requirements.txt → Python/Django/Flask
go.mod          → Go
Cargo.toml      → Rust
```

State what you found:
```
STACK DETECTED:
- React 19.1.0 (from package.json)
- Vite 6.2.0
→ Fetching official docs for relevant patterns.
```

If versions are ambiguous → **ASK**. Don't guess.

### Step 2: Fetch Official Documentation

**Source hierarchy (in order of authority):**

| Priority | Source | Example |
|----------|--------|---------|
| 1 | Official documentation | react.dev, docs.djangoproject.com |
| 2 | Official blog / changelog | react.dev/blog |
| 3 | Web standards references | MDN, web.dev |
| 4 | Browser/runtime compatibility | caniuse.com |

**NOT authoritative — never cite as primary:**
- Stack Overflow answers
- Blog posts or tutorials
- AI-generated summaries
- Your own training data

### Step 3: Implement Following Docs

- Use API signatures from docs, not from memory
- If docs show a new way → use the new way
- If docs deprecate a pattern → don't use it
- If docs don't cover something → flag as unverified

**When docs conflict with existing code:**
```
CONFLICT DETECTED:
Existing code uses useState for form loading state,
but React 19 docs recommend useActionState.
(Source: react.dev/reference/react/useActionState)

Options:
A) Use modern pattern — consistent with docs
B) Match existing code — consistent with codebase
→ Which approach?
```

### Step 4: Cite Your Sources

```typescript
// React 19 form handling with useActionState
// Source: https://react.dev/reference/react/useActionState#usage
const [state, formAction, isPending] = useActionState(submitOrder, initialState);
```

If you cannot verify:
```
UNVERIFIED: Could not find official documentation for this pattern.
Based on training data — may be outdated. Verify before production.
```

---

## Common Rationalizations

| Rationalization | Reality |
|---|---|
| "I'm confident about this API" | Confidence ≠ evidence. Training data has outdated patterns. Verify. |
| "Fetching docs wastes tokens" | Hallucinating APIs wastes more. One fetch prevents hours of rework. |
| "This is simple, no need to check" | Simple tasks with wrong patterns become templates copied everywhere. |
| "I'll just mention it might be outdated" | A disclaimer doesn't help. Either verify + cite, or flag as unverified. |

---

## Verification

- [ ] Framework versions identified from dependency file
- [ ] Official docs fetched for framework-specific patterns
- [ ] All sources are official documentation (not blogs or training data)
- [ ] Code follows current version's documented patterns
- [ ] Non-trivial decisions include source citations with full URLs
- [ ] No deprecated APIs used
- [ ] Anything unverified is explicitly flagged
