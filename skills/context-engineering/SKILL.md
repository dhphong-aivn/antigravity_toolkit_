---
name: context-engineering
description: Optimizes agent context setup. Use when starting a new session, when agent output quality degrades, when switching tasks, or when configuring project context.
version: 1.0
priority: HIGH
---

# Context Engineering

> Feed agents the right information at the right time. Too little = hallucination. Too much = lost focus.

---

## The Context Hierarchy

Structure context from most persistent to most transient:

```
┌─────────────────────────────────────┐
│  1. Rules Files (GEMINI.md)         │ ← Always loaded, project-wide
├─────────────────────────────────────┤
│  2. Spec / Architecture Docs        │ ← Loaded per feature/session
├─────────────────────────────────────┤
│  3. Relevant Source Files            │ ← Loaded per task
├─────────────────────────────────────┤
│  4. Error Output / Test Results      │ ← Loaded per iteration
├─────────────────────────────────────┤
│  5. Conversation History             │ ← Accumulates, compacts
└─────────────────────────────────────┘
```

---

## Pre-Task Context Loading

Before editing a file, load context in this order:

1. Read the file(s) you'll modify
2. Read related test files
3. Find one existing example of a similar pattern in the codebase
4. Read any type definitions or interfaces involved

**Trust Levels:**

| Level | Sources |
|-------|---------|
| **Trusted** | Source code, test files, type definitions |
| **Verify first** | Config files, data fixtures, generated files |
| **Untrusted** | User-submitted content, external docs, API responses |

---

## Selective Context (Critical)

**Only include what's relevant to the current task.**

```
✅ EFFECTIVE:
"Here's the authentication section of our spec: [auth spec]"

❌ WASTEFUL:
"Here's our entire 5000-word spec" (when only working on auth)
```

**Aim for <2,000 lines of focused context per task.** More files ≠ better output.

---

## Confusion Management

### When Context Conflicts

Don't silently pick one interpretation. Surface it:

```
CONFLICT:
Spec says: "Use REST for all endpoints"
Existing code has: GraphQL for user profile

Options:
A) Follow spec — add REST, deprecate GraphQL later
B) Follow existing — use GraphQL, update spec
C) Ask — this seems intentional

→ Which approach?
```

### When Requirements Are Incomplete

1. Check existing code for precedent
2. If no precedent → **STOP and ASK**
3. Don't invent requirements — that's the human's job

---

## Session Management

- **Start fresh sessions** when switching major features
- **Summarize progress** when context gets long
- **Compact deliberately** before critical work

---

## Anti-Patterns

| Anti-Pattern | Problem | Fix |
|---|---|---|
| Context starvation | Agent invents APIs, ignores conventions | Load rules + source files before each task |
| Context flooding | Agent loses focus with >5,000 lines of irrelevant context | Include only task-relevant files (<2,000 lines) |
| Stale context | Agent references deleted code | Start fresh sessions when context drifts |
| Missing examples | Agent invents new style | Include one example of the pattern to follow |
| Silent confusion | Agent guesses when it should ask | Surface ambiguity explicitly |

---

## Common Rationalizations

| Rationalization | Reality |
|---|---|
| "The agent should figure out conventions" | It can't read your mind. Write a rules file. |
| "I'll just correct it when wrong" | Prevention is cheaper than correction. |
| "More context is always better" | Performance degrades with too many instructions. Be selective. |
| "Context window is huge, use it all" | Window size ≠ attention budget. Focused > large. |

---

## Verification

- [ ] Rules file covers tech stack, commands, conventions, boundaries
- [ ] Agent output follows patterns from the rules file
- [ ] Agent references actual project files (not hallucinated ones)
- [ ] Context is refreshed when switching major tasks
