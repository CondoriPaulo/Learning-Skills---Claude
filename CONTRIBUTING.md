# Contributing to Learning Skills Claude

Thanks for wanting to improve these skills! We're building a library that works *with* the ADHD brain, not against it.

---

## What We're Looking For

### 🐛 Bug Reports
- A skill doesn't trigger when it should
- A handoff breaks (e.g., STEM Learning App → Math Fluency Drill doesn't work)
- Output content has errors or typos
- A guideline in SKILL.md isn't being followed

**How to report:**
1. Open an issue with the skill name, what you tried, and what happened
2. Include a screenshot or example input if possible
3. No blame — these are complex systems

### 💡 Feature Requests
- New gamification mechanic (e.g., "add achievement badges")
- New skill entirely (e.g., "Scientific paper critic")
- Better handling of a specific STEM topic
- Additional accessibility feature (e.g., "add high-contrast theme toggle")

**How to suggest:**
1. Open an issue with "[FEATURE]" in the title
2. Explain the problem it solves
3. Give an example of how you'd use it

### ✏️ Improvements to Existing Skills
- Better explanations in SKILL.md
- New problem types for Math Fluency Drill
- Additional color schemes for Study from Lecture
- More robust hardening techniques for STEM Learning App

---

## How to Contribute Code/Content

### 1. Fork the repo
```
git clone https://github.com/CondoriPaulo/Learning-Skills---Claude.git
cd Learning-Skills---Claude
```

### 2. Create a branch
```
git checkout -b skill/your-improvement-name
```

(Examples: `skill/stem-app-fixes`, `skill/new-color-scheme`, `feature/achievement-system`)

### 3. Edit the skill
- **SKILL.md** — the teaching/building instructions
- **README.md** — the user-facing concise reference

Keep SKILL.md aligned with SKILL.md documentation style:
- Short sentences
- Concrete examples
- Clear hierarchy (## headers for sections)
- Code blocks for technical details

### 4. Test Your Changes
- **If you're improving a skill**, open Claude and test the new version against a sample input (e.g., a sample PDF for STEM Learning App)
- **If you're adding a new problem type**, make sure it follows the hard rules (concrete, no timers, strategy naming, etc.)
- **Document what you tested** in your PR description

### 5. Submit a Pull Request
- Title: `[skill-name] Brief description` (e.g., `[math-fluency-drill] Add fix-the-error problem type`)
- Description: what changed, why, and what you tested
- Link any related issues

Example PR description:
```
## Changes
- Added "fix-the-error" problem type to Math Fluency Drill
- Updated SKILL.md with example format

## Why
Students respond well to error-spotting (medium/hard stage). Provides strategy variety.

## Tested
- 5 example problems generated
- Verified re-queue and session wrap-up still work
- Tested on phone viewport (380px)
```

---

## Style Guide

### SKILL.md Writing
- **Short sentences** — max 20 words per sentence for complex ideas
- **One idea per bullet** — never two concepts in one bullet
- **Concrete > abstract** — "the loss function decreased" not "optimization improved"
- **Show examples** — pseudocode, diagrams, sample outputs
- **Explain the why** — not just the what, but why this design choice matters

### README.md Writing
- **Scannable** — short sections, clear headers
- **Benefits over features** — "you control pacing" not "user-configurable timing"
- **Real examples** — *"make me a STEM learning game from this PDF"* not *"create interactive content"*
- **Keep under 200 words** per README (concise reference style)

### Code Examples in SKILL.md
```javascript
// Use code blocks for clarity
// Explain what's happening in the comment above

// Good: clear, short
function bionicWord(w) {
  var n = Math.max(1, Math.round(w.length * 0.45));
  return w.slice(0, n) + "bold..." + w.slice(n);
}

// Bad: too much explanation inline, not in comments above
const thresholdValue = 0.3; // the threshold we use for soft thresholding
```

---

## Principles We Won't Compromise On

1. **Teach before test** — never quiz first, explain later
2. **No timers** — ever. Pressure kills fluency
3. **Concrete always** — no abstract placeholders
4. **Spaced retrieval** — re-queue missed problems, don't immediate re-drill
5. **Hyperfocus baiting** — most interesting content first, not document order
6. **Tangent harvesting** — curiosity is a feature, not a bug
7. **Progressive enhancement** — if JavaScript breaks, content is still readable

If your contribution violates one of these, we'll ask you to revise. This isn't opinion — it's science (Bjork, Brown, Dweck, ADHD research).

---

## Questions?

- **How do I locally test a skill?** Open Claude, paste the SKILL.md content into a system prompt, and feed it a sample input
- **Can I add a completely new skill?** Absolutely — open a [FEATURE] issue first to discuss scope and design
- **What if I disagree with a principle?** Open an issue tagged [DISCUSSION] and let's talk. Science might disagree with both of us

---

## Recognition

We'll add your name and contribution to a CONTRIBUTORS.md file. No anonymity unless you request it.

---

**Thank you for making learning tools that actually work for how brains learn.** 🧠

—Paulo Condori Pinedo & the Learning Skills community
