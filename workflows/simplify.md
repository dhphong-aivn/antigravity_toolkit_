---
description: Simplify code for clarity and maintainability. Reduce complexity without changing behavior. Surgical, incremental changes.
---

# /code-simplify - Code Simplification

$ARGUMENTS

---

## 🔴 CRITICAL RULES

1. **Behavior MUST NOT change** — Same inputs = same outputs, always
2. **Tests MUST pass** — Before AND after every single change
3. **Incremental changes** — One simplification at a time, verify after each
4. **Revert if tests fail** — Don't force broken simplifications
5. **Surgical changes only** — Don't "improve" adjacent unrelated code

---

## Task

### Step 1: Understand Before Touching

Before changing anything:

- Read the target code thoroughly
- Identify callers, dependents, and downstream effects
- Check existing test coverage — if no tests exist, write them FIRST
- Understand WHY the code exists (Chesterton's Fence principle)

> 🛑 If you don't understand why code exists, ASK before removing/changing it.

### Step 2: Scan for Opportunities

| Pattern Found | Simplification |
|---------------|---------------|
| Deep nesting (3+ levels) | Guard clauses or extract helper function |
| Long function (50+ lines) | Split by single responsibility |
| Nested ternaries | Replace with `if/else` or `switch` |
| Generic names (`data`, `temp`, `val`, `x`) | Use descriptive names |
| Duplicated logic (3+ occurrences) | Extract shared function |
| Dead code (YOUR changes made it dead) | Remove it |
| Pre-existing dead code | MENTION it, don't delete |
| Over-abstraction (used only once) | Inline it |
| Unnecessary wrapper functions | Remove wrapper, call directly |
| Complex boolean expressions | Extract to named variable |

### Step 3: Apply Incrementally

For EACH simplification:

```
1. Make one change
   → verify: Tests still pass
2. Run build
   → verify: No compilation errors
3. Check diff
   → verify: Only intended lines changed (Surgical Changes rule)
4. Move to next simplification
```

If tests fail after ANY change → **Revert immediately** and reconsider approach.

### Step 4: Final Verification

- [ ] All tests pass ✅
- [ ] Build succeeds ✅
- [ ] Diff is clean — no unrelated changes ✅
- [ ] Behavior unchanged — same inputs produce same outputs ✅
- [ ] Code is measurably simpler (fewer lines, lower complexity) ✅

### Step 5: Report

```markdown
## ✂️ Simplification Report: [Target]

### Changes Made
| # | What | Before | After | Lines Saved |
|---|------|--------|-------|-------------|
| 1 | Extracted guard clause | 5-level nesting | Early return | -8 lines |
| 2 | Renamed variables | `d`, `tmp` | `userData`, `tempFile` | 0 lines |

### Metrics
- Lines before: X
- Lines after: Y
- Reduction: Z%
- Tests: All passing ✅

### Not Changed (Intentional)
- [List things you noticed but didn't touch, and why]
```

---

## Karpathy Principles Applied

> "If you write 200 lines and it could be 50, rewrite it."

> "Every changed line should trace directly to the user's request."

> "Don't refactor things that aren't broken."

---

## Anti-Rationalization

| Excuse | Rebuttal |
|--------|----------|
| "I'll refactor everything while I'm here" | ONLY simplify what was asked. Surgical changes. |
| "Tests are overkill for renaming" | Run tests after EVERY change. No exceptions. |
| "This abstraction might be useful later" | YAGNI. If it's used once, inline it now. |
| "The existing code style is wrong" | Match existing style. Propose style changes separately. |
| "I can skip tests, this is obviously safe" | "Obviously safe" changes cause the worst bugs. Test always. |

---

## Usage

```
/code-simplify src/services/payment.ts
/code-simplify recently changed files
/code-simplify src/utils/
/code-simplify src/components/Dashboard.tsx
```
