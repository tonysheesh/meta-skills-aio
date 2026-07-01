# 🧩 Meta-Skills AIO

> One skill, nine modules, running on every message to lift Claude's output quality, context retention, and usefulness — with zero visible overhead.

---

## 🧠 What it does

Each module activates only when its trigger condition is met — not all nine run on every message, but the router checks every time.

| # | Module | Triggers on |
|---|---|---|
| 1️⃣ | 🧭 **Skill Router** | Every message — finds or auto-creates missing skills |
| 2️⃣ | ✨ **Prompt Optimizer** | Vague, short, or ambiguous requests |
| 3️⃣ | 🗂️ **Task Decomposer** | Multi-step, multi-deliverable, or unclear sequencing |
| 4️⃣ | 🔍 **Assumption Auditor** | High-effort tasks where a wrong guess = full redo |
| 5️⃣ | ✅ **Output Quality Checker** | Every substantive deliverable |
| 6️⃣ | 📄 **Context Summarizer** | Threads over ~15 messages or far-back references |
| 7️⃣ | 🧠 **Memory Manager** | End of conversations with retainable facts |
| 8️⃣ | 💡 **Follow-Up Generator** | After any significant deliverable |
| 9️⃣ | 💰 **Token Optimizer** | Every message — output discipline + cost routing |

---

## 🧭 Module 1 — Skill Router

Checks `available_skills` before responding. If something relevant is missing, **builds it on the spot** — no permission asked:

```bash
cd /mnt/skills/examples/skill-creator && python -m scripts.package_skill /home/claude/{skill-name}/ /home/claude/output/
```

Minimum 80 lines: frontmatter, purpose, inputs, workflow, output format, quality checklist, examples, edge cases.

---

## ✨ Module 2 — Prompt Optimizer

Silently rewrites vague requests into their highest-performing form, states it in one line:
> *"Interpreting as: [rewritten prompt]"*

Then executes — no confirmation needed unless the reinterpretation is dramatic.

---

## 🗂️ Module 3 — Task Decomposer

For 3+ step tasks, produces a brief plan before executing:
```
Plan:
1. [step] → [output]
2. [step] → [output]
```

---

## 🔍 Module 4 — Assumption Auditor

One line, only when a wrong guess would be costly:
> *Assuming: [X], [Y], [Z]. Proceeding — correct me if wrong.*

---

## ✅ Module 5 — Output Quality Checker

Internal checklist before shipping any deliverable — answers the actual question, no vague filler, correct format, claims supported, nothing missing, right length.

---

## 📄 Module 6 — Context Summarizer

Prepends a compressed brief (≤6 lines) when threads run long:
```
── Thread Brief ──────────────────────────────
Goal: ...
Decisions made: ...
Current state: ...
Pending: ...
─────────────────────────────────────────────
```

---

## 🧠 Module 7 — Memory Manager

At natural conversation end points, surfaces a memory-save suggestion:
```
── Memory Update ─────────────────────────────
Add to memory:
• [fact / preference / decision]
─────────────────────────────────────────────
```

---

## 💡 Module 8 — Follow-Up Generator

One specific, high-value next action after a deliverable:
> 💡 **Next:** [action the user probably hasn't thought of]

Skipped entirely if there's nothing genuinely valuable to add.

---

## 💰 Module 9 — Token Optimizer

Always-on output discipline: strict length matching, no restating the question, files instead of walls of text, no "let me know if you need anything else."

Also flags long threads for summarize-and-restart, strips noise from large pastes, and routes cost — e.g. suggesting Haiku for simple Q&A on the API.

**Estimated savings: 40–80% per session** through output discipline alone.

---

## 🚦 Behavior Rules

- 🤫 **Silent by default** — modules don't announce themselves unless their output is user-visible
- 1️⃣ **One-line surface** — minimum footprint when a module does produce output
- 🚫 **Never blocks** the actual answer — meta-processing accelerates, never delays
- 🧵 **No stacked ceremony** — multiple triggered modules merge naturally into one clean response
- 🎨 **Respects user preferences** — formatting rules apply to meta-output too

---

## 📤 Example: Full Stack in Action

**User:** "build me a landing page"

```
Skill Router      → frontend-design ✓, canvas-design ✓
Prompt Optimizer  → "Interpreting as: single-page HTML landing page,
                     modern, responsive, no framework specified"
Assumption Auditor→ "Assuming: no brand colors/copy — using placeholders."
Task Decomposer   → [silently plans: layout → content → styling → artifact]
[executes]
Output Quality    → [internal check passes]
Follow-Up         → "💡 Next: drop your brand hex codes — I can restyle
                     the whole page in one message."
```

What the user sees: one clean response, a working landing page, a one-line assumption note, one useful next step. **No meta-noise.**

---

## 📦 Install

```bash
npx skills add ./meta-skills-aio
```

Or upload via **Claude.ai → Settings → Features → Custom Skills**.

---

<p align="center">Nine systems. One skill. Invisible until it matters.</p>
