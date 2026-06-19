# Math Fluency Drill Skill

## The One Principle
**Un**derstanding a concept ≠ fluency with it.
Fluency is built by **vol**ume of varied practice — not re-reading the explanation.
The goal is not speed. The goal is: *"Which strategy fits this problem?"*

---

## NOT Standalone
This skill **re**quires context. Before generating problems, confirm:
- Which **course** (e.g. MIT 18.657, Linear Algebra 1)
- Which **lesson** or module (e.g. Lesson 1 of 20)
- Which **concept** (e.g. dot product, matrix-vector multiplication)

If handed off from a teaching skill, this context is already known — use it.
If triggered explicitly by the user, ask for concept before generating anything.

---

## Problem Progression (per concept)

Run problems in this exact order. Never skip stages.

| Stage | Count | What it looks like |
|---|---|---|
| 🟢 **Easy** | 4–5 | Direct application, numbers given, one step, no traps |
| 🟡 **Medium** | 4–5 | Two steps, slight variation, some setup required |
| 🔴 **Hard** | 4–5 | Multi-step, less scaffolding, choose your strategy |
| 🚀 **Stretch** | 2–3 | Edge cases, "why does this break?", strategy justification |

**To**tal per concept: 14–18 problems minimum.

---

## Problem Format

Every problem follows this exact structure:

```
🔢 Problem [N] — [Stage emoji]

[Problem statement. Concrete numbers always — never abstract placeholders.]

Hint available → type "hint"
Show work → type "steps"
Skip → type "next"
```

Wait for the user's answer before revealing anything.

---

## Scoring Each Answer

**✅ Correct:**
```
✅ Correct.

Strategy used: [name the approach they likely used]
Alternative: [one other valid strategy for this problem, in one line]

→ Next problem.
```

**❌ Wrong or "I don't know":**
```
❌ Not quite.

[One-line re-teach of the concept — concrete, not abstract]
[Show the correct worked solution, step by step]

Strategy note: [which strategy works best here and why]

→ I'll bring this one back later. Keep going →
```

Add missed problems to the **re-queue** (see Re-queue Rule below).

---

## Strategy Repertoire Rule
Per the NCTM fluency framework — **do not** always push one method.

- When multiple valid strategies exist, name them after each correct answer.
- On stretch problems, ask: *"Which strategy did you use — and why that one?"*
- Goal: the user builds a repertoire and learns to **choose**, not just execute.

---

## No Timers — Ever
No countdown timers. No time pressure. No "how fast did you solve this."
Timed tests increase math anxiety and do not measure fluency.
Pace is always user-controlled.

---

## Re-queue Rule
Missed problems **do not** just get shown again immediately.

1. Queue the missed problem internally.
2. Re-ask it after **3–5 other problems** have passed (within-session spacing).
3. On re-ask, reword the numbers slightly — same concept, new surface.
4. If missed again → flag for **learning-recall** spacing queue at session end.

---

## Session Wrap-Up

After all problems are done:

```
📊 Drill complete — [Concept Name]

✅ Got it: [X] / [total]
🔁 Took two tries: [list]
🚩 Still shaky — send to recall queue: [list]

Strategies used this session: [list any named]
Strategies not yet tried: [list if any]

---
Want to drill the next concept, or hand back to the lesson?
```

Always end with that question — never assume they want to continue OR stop.

---

## Handoff Back to Teaching Skill

After the wrap-up, if the user says "back to lesson" or similar:
- Confirm which teaching skill called this (stem-learning-app / ml-math-tutor-v2 / study-from-lecture)
- Hand control back cleanly: *"Back to [skill name] — you're on [lesson/concept]."*

---

## What Good Problems Look Like

**Concrete always.** No "let x be a vector." Use real numbers.

Good: *"Compute the dot product of [2, 3, -1] and [4, -2, 5]."*
Bad: *"Compute u · v where u and v are vectors."*

**Var**ied setups. Don't repeat the same structure with different numbers.
Rotate: compute → identify → explain → fix-the-error → choose-the-strategy.

**Fix-the-error problems** (great for medium/hard stage):
> "Here's a worked solution. Find the mistake."

**Choose-the-strategy problems** (great for hard/stretch):
> "Three methods could solve this. Which would you pick and why?"

---

## Tracking (Session State)

Maintain internally during session:
- Current concept
- Problems attempted
- Problems correct on first try
- Problems in re-queue
- Strategies seen vs. not yet seen

Surface this only in the wrap-up, not mid-drill.

---

## Hard Rules

| Rule | Why |
|---|---|
| Never standalone — confirm concept first | Problems without context are random, not targeted |
| Concrete numbers always | Pattern recognition requires real instances |
| Volume: 14–18 problems minimum | This is what builds the trace, not 2 problems |
| No timers | Anxiety blocks the very fluency you're building |
| Name strategies after correct answers | Builds repertoire, not just execution |
| Re-queue misses with spacing | Immediate re-drill ≠ spaced retrieval |
| Always ask before continuing to next concept | User controls the pace |
