# Learning Skills Claude

**Open-source Claude skills for ADHD-friendly, interactive learning.**

A curated library of five interconnected skills that transform static educational content (PDFs, slides, lectures) into self-contained, interactive HTML learning apps with gamification, spaced recall, and adaptive feedback loops.

---

## Why This Exists

**Learning ≠ reading.** Real learning requires:
- **Teach-first flows** (explanation before assessment)
- **Worked examples** (step-by-step, concrete)
- **Spaced retrieval** (not cramming)
- **Bionic reading + visual aids** (for ADHD brains)
- **Procedural fluency** (volume of varied practice, not one-shot understanding)

These skills embed that science into every interaction.

---

## The Five Skills

| Skill | Purpose | Input | Output |
|-------|---------|-------|--------|
| **STEM Learning App** | Transform static STEM material into interactive HTML course | PDF, slides, lecture notes | Self-contained `.html` learning app with XP, streaks, quiz flow |
| **ML Math Tutor v2** | Anchor ML math (linear algebra, calculus, optimization) to *your code* | Assignment + code + dataset | Block-by-block teaching + quiz + fluency drill handoff |
| **Math Fluency Drill** | Build procedural fluency through progressive problem sets | Concept name (after teaching) | 14–18 problems, ramping easy→stretch, with re-queue on miss |
| **Study from Lecture** | Extract key concepts + visuals from academic material | PDF, slides, notes | Visual concept map + color-coded Q&A + cheat sheet |
| **Learning Recall** | Cement knowledge through forced retrieval (active recall) | Paper, slides, notes (already seen) | Blank-page recall targets + spacing schedule |

---

## How They Connect

```
Raw material (PDF, slides, lecture)
    ↓
[STEM Learning App or Study from Lecture] — teach the concept
    ↓
[Math Fluency Drill] — build procedural fluency (optional handoff)
    ↓
[Learning Recall] — lock it in long-term (1 day → 3 days → 1 week)
```

Each skill has a **handoff button** — when you complete a teaching skill, it offers: *"Want to drill this?"* or *"Want to test recall?"* No forced flow; user controls the pace.

---

## Getting Started

### Option 1: Simple Chat (Recommended for quick learning)
1. Open Claude (claude.ai or Claude app)
2. Upload your material (PDF, slides, notes)
3. Type: `"Make this into an interactive STEM learning app"` or `"Help me study this"`
4. Claude auto-selects the right skill based on your request

### Option 2: Claude Code (For DevEx / custom builds)
If you want to **extend or remix** these skills:
1. Open Claude Code (terminal, VS Code, or JetBrains)
2. Clone this repo
3. Edit the skill SKILL.md files (they're plain text)
4. Create a local Claude skill from your version
5. Test in Claude chat
6. Push your improvements back (see CONTRIBUTING.md)

### Option 3: Offline + Mobile
Each STEM Learning App output is a **single .html file** that:
- Works completely offline (no internet after download)
- Opens on phones (iOS Quick Look, Android browser) with full functionality
- Renders instantly — no build step

---

## Philosophy

### 🧠 ADHD-Friendly by Design
- **Chunked, not paragraphs** — max 3 bullets per concept
- **Hyperfocus baited, not summoned** — most interesting topic first
- **Tangents harvested, not suppressed** — curiosity is a feature
- **Bionic reading + dark mode** — high contrast, fast scanning
- **Fast feedback loops** — XP every 30–60s, not at session end

### 📚 Spaced Retrieval, Not Cramming
- Teaching → Quiz → Fluency Drill → Recall (next day, 3 days, 1 week)
- Spacing is science; cramming is theater
- Memory is built by retrieval, not re-reading

### 🎯 Teach Before Test
- Every quiz question comes *after* explanation + worked example
- Wrong answers trigger re-teaching (study-from-lecture style), not just revealing the answer
- If you get it wrong, you learn why

### 🎮 Gamification With Purpose
- XP, levels, streaks, confetti — all timed for dopamine hits
- Progress bar visible; rank names are encouraging
- None of it feels like gamification; it just works

---

## Contributing

See **CONTRIBUTING.md** for how to:
- Report bugs or request new skills
- Fork and adapt skills for your own learners
- Submit improvements (better explanations, new concepts, edge cases)
- Add translations

---

## Tech Stack

- **Skills are pure markdown + JSON** (SKILL.md files) — no code required to edit
- **Output is vanilla HTML + JS** — runs on any browser, offline, no dependencies
- **Claude API integration** — each skill calls Claude's API when building content (no locked services)

---

## License

MIT — fork, adapt, remix, use in your own projects.

---

## Questions?

- **How do I adapt a skill for my students?** → Fork the repo, edit the SKILL.md, test in Claude.
- **Can I use these with other LLMs?** → These are Claude-specific (use Claude SDK or API). If you want GPT versions, fork and adapt.
- **Do these skills work offline?** → STEM Learning App outputs are fully offline. Skill invocation requires Claude (online).
- **Can I contribute a new skill?** → Yes! See CONTRIBUTING.md.

---

**Built by Paulo Condori Pinedo.** Maintained with ❤️ for learners who think in pictures, chase tangents, and deserve learning tools that work *with* their brain, not against it.
# Learning-Skills---Claude
