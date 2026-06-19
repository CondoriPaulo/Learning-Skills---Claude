# Math Fluency Drill

**Build procedural fluency through spaced, progressive problem sets. Not for first-time learning — only after teaching.**

## What It Does

Generates 14–18 problems per concept, ramping from easy → hard → stretch:
- **🟢 Easy** (4–5): Direct application, numbers given, no traps
- **🟡 Medium** (4–5): Two steps, slight variation, some setup
- **🔴 Hard** (4–5): Multi-step, less scaffolding, choose your strategy
- **🚀 Stretch** (2–3): Edge cases, "why does this break?", strategy justification

## Key Features

- **Volume-based fluency** — not understanding (which comes from teaching), but *recognizing* which strategy fits *this problem*
- **Re-queue on miss** — wrong problems come back after 3–5 other problems (spaced retrieval), reworded slightly
- **Strategy naming** — after each correct answer, Claude names the approach used + mentions an alternative
- **Concrete always** — real numbers, never abstract placeholders
- **No timers** — ever. Pressure kills fluency; pacing is user-controlled
- **Problem variance** — compute → identify → explain → fix-the-error → choose-strategy
- **Session wrap-up** — shows problems got first try vs. took two tries vs. still shaky

## When to Use

- After completing a **STEM Learning App** concept quiz (handoff: *"Drill this?"*)
- After an **ML Math Tutor v2** quiz block (handoff)
- After a **study-from-lecture** session (explicit handoff)
- Any time: *"I need practice problems on [concept]"*

## NOT Standalone

This skill **requires prior teaching context**. Before generating problems, must confirm:
- Which **course / lesson** (e.g., "MIT 18.657 Linear Algebra")
- Which **concept** (e.g., "dot product", "matrix-vector multiplication")

If triggered standalone (user says "drill me" without context), ask for concept first.

## Output

14–18 problems, progressive difficulty, re-queue on miss, session summary with spacing guidance.

## What's Special

**Strategy repertoire** — not one method repeated. Names multiple valid strategies, asks students to *choose* which one fits.

**Missed problems come back later** — not immediate re-drill. After ~3–5 problems, reworded version of the missed one. Actual spaced retrieval, not cramming.

**Wrap-up includes spacing schedule** — tells you: re-do this in ~1 day, then ~3 days, then ~1 week. That's what locks it in.

## Handoff

After wrap-up, always asks: *"Drill next concept, or back to lesson?"* — user controls flow, no forced continuation.

---

See SKILL.md for problem progression, scoring, re-queue mechanics, and session state tracking.
