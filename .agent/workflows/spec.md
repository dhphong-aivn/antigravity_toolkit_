---
description: Spec-driven development. Write a structured specification (SPEC.md) before writing any code.
---

# /spec - Specification First

$ARGUMENTS

---

## 🔴 CRITICAL RULES

1. **NO CODE WRITING** - This command creates SPEC.md only
2. **Ask before assuming** - Apply "Think Before Coding" principle
3. **Output file** - Save as `docs/SPEC-{task-slug}.md`
4. **User confirmation** - Do NOT proceed to code until spec is approved

---

## Task

### Phase 1: Discovery (Mandatory)

Ask clarifying questions about:

1. **Objective** — What problem does this solve? Who are the users?
2. **Core Features** — What are the must-have features? What's out of scope?
3. **Tech Stack** — Any preferences or constraints?
4. **Acceptance Criteria** — How do we know it's done?
5. **Boundaries** — What should we ALWAYS do, ASK FIRST about, NEVER do?

> 🛑 Do NOT skip this phase. If even 1% is unclear, ASK.

### Phase 2: Spec Generation

After user answers, generate `docs/SPEC-{task-slug}.md` with this structure:

```markdown
# SPEC: {Title}

## 1. Objective
[What problem this solves and why it matters]

## 2. Target Users
[Who will use this and their primary needs]

## 3. Core Features
- Feature A: [description] → Acceptance: [criteria]
- Feature B: [description] → Acceptance: [criteria]
- Feature C: [description] → Acceptance: [criteria]

## 4. Out of Scope
[What this does NOT include — prevents scope creep]

## 5. Tech Stack
[Framework, language, dependencies, reasoning]

## 6. Project Structure
[Proposed directory layout]

## 7. Code Style & Conventions
[Naming, patterns, formatting rules]

## 8. Testing Strategy
[What to test, coverage goals, test types]

## 9. Boundaries
- ALWAYS: [hard rules]
- ASK FIRST: [gray areas that need user input]
- NEVER: [absolute limits]

## 10. Success Criteria
[How do we verify the spec is fully implemented?]
```

### Phase 3: Confirmation

Present spec to user for review. Ask:
- "Does this capture your vision?"
- "Anything to add, change, or remove?"

---

## Naming Rules

1. Extract 2-3 key words from request
2. Lowercase, hyphen-separated
3. Max 30 characters

| Request | Spec File |
|---------|-----------|
| `/spec e-commerce cart` | `docs/SPEC-ecommerce-cart.md` |
| `/spec user auth system` | `docs/SPEC-user-auth.md` |
| `/spec dark mode feature` | `docs/SPEC-dark-mode.md` |

---

## After Spec

Tell user:
```
✅ Spec created: docs/SPEC-{slug}.md

Next steps:
- Review and edit the spec
- Run `/plan` to break down into tasks
- Or run `/create` to start building
```

---

## Anti-Rationalization

| Excuse | Rebuttal |
|--------|----------|
| "This is too small for a spec" | Small specs = fast to write. Still create one. |
| "I already understand the requirements" | The USER needs to confirm. Write it down. |
| "Let me just start coding" | Code without spec = rework. Spec first. |
| "The user was clear enough" | Clarity in conversation ≠ clarity in implementation. Document it. |

---

## Usage

```
/spec e-commerce shopping cart
/spec REST API for user management
/spec dark mode toggle feature
/spec mobile fitness tracker
```
