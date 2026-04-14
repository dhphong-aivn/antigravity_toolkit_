# Antigravity Kit (Custom Developer Edition)

> 🚀 AI Agent templates enhanced with strict behavioral rules, customized Skills, and optimized Workflows for advanced AI-assisted development.

**Credit & Origin:** This is a customized version tailored for specific development flows. The original toolkit repository was created by the author **vudovn** (Original project: [Antigravity Kit](https://unikorn.vn/p/antigravity-kit)).

---

## 🎯 What's New in This Custom Version

This developer edition introduces additional strict enforcement rules and principles (inspired by Karpathy and Addy Osmani) to minimize AI hallucinations and maximize code quality:

- **Anti-Rationalization Engine:** Prevents the AI from making excuses (e.g., "I'll fix tests later") or bypassing essential quality gates.
- **Surgical Changes Protocol:** Enforces minimal, strictly necessary code diffs without risky "drive-by" refactoring.
- **Goal-Driven Execution:** Forces validation loops before the AI can confirm a task is completed.
- **Source-Driven Development:** Requires the AI to fetch official framework documentation (React 19, Next.js 15, etc.) instead of relying on outdated training memory.
- **Context Engineering:** Strictly limits context bloating to keep the AI focused and accurate.

---

## 📦 Quick Install (Custom Edition)

Bởi vì đây là phiên bản cá nhân hóa (Origin), bạn không dùng `npx` như bộ gốc. Để mang bộ kỹ năng này áp dụng cho bất kỳ project mới nào của bạn:

```bash
# 1. Clone repo chứa bộ Toolkit tùy chỉnh của bạn về máy
git clone https://github.com/your-username/your-repo-name.git

# 2. Copy toàn bộ thư mục lõi vào trong project mới mà bạn muốn làm việc
cp -r your-repo-name/.agents /path/to/your/new-project/
```

> **⚠️ Lưu ý quan trọng cho Cursor / Windsurf:**
> Đảm bảo rằng thư mục `.agents` **KHÔNG** nằm trong file `.gitignore` của project mới. Hãy đưa nó vào `.git/info/exclude` để IDE có thể index được hệ thống các lệnh `/slash`.

---

## 📋 Toolkit Structure

The toolkit operates through a robust taxonomy of instructions:

| Component | Count | Function |
| :--- | :---: | :--- |
| **Agents** | 20 | Specialist AI personas with distinct boundaries (e.g., `frontend-specialist`, `database-architect`, `security-auditor`). |
| **Skills** | 38 | Domain-specific knowledge modules that agents equip dynamically (e.g., `clean-code`, `testing-patterns`). |
| **Workflows** | 14 | Standardized operational procedures via slash commands. |

## ⚙️ Intelligent Routing (How it works)

You do not need to manually explicitly mention agents for every task. The core engine (`GEMINI.md` / `intelligent-routing`) automatically detects your intent:

```text
User: "Refactor the database schema to support many-to-many users and roles."
AI: 🤖 Applying knowledge of @database-architect + @clean-code...
```

1. **Domain Detection:** Silently analyzes if the request belongs to Frontend, Backend, DevOps, or QA.
2. **Modular Skill Injection:** Loads only the requested rules, keeping the AI's context window extremely clean.
3. **Mandatory Socratic Gate:** If a request is vague, the AI will refuse to code and ask clarifying questions first.

## 🚀 Workflows (Slash Commands)

Use standard slash commands to trigger structured AI processes:

| Command | Lifecycle Phase | Purpose |
|---------|-----------------|---------|
| `/brainstorm` | Discovery | Socratic discovery and clarification before building. |
| `/spec` | Planning | Write technical specifications and constraints. |
| `/plan` | Planning | Generate an actionable checklist and architecture plan. |
| `/create` | Execution | Generate a new feature or full project from scratch. |
| `/review` | Validation | Perform a 5-axis code review on existing code. |
| `/debug` | Maintenance | Systematic debugging and root-cause analysis. |

## 🛠 Script Verifications

Instead of trusting the AI's "word" that code works, this toolkit forces agents to use Python validation scripts to empirically prove success:

- `test_runner.py` / `lint_runner.py` (Functional checks)
- `security_scan.py` / `schema_validator.py` (Structural checks)
- `ux_audit.py` / `accessibility_checker.py` (UI/UX checks)

---
## ⚖️ License

Original core logic and boilerplate by **Vudovn** under the MIT License. Custom extensions maintain the same spirit of open developer tooling.
