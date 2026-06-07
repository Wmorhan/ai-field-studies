# Design: Scaling Your Configuration

**Date:** 2026-06-07  
**Output file:** `lessons/05-advanced/configuration-strategies.md`  
**Role:** Advanced lesson — assumes reader has completed `lessons/01-getting-started/configure-claude-md.md`

---

## Purpose

Readers who've mastered basic CLAUDE.md configuration hit two scaling problems: tool lock-in (CLAUDE.md only works with Claude Code) and single-file limits (one config can't cover a monorepo with multiple distinct apps). This lesson names both problems and gives the practical fix for each. Kept deliberately simple — expandable later.

---

## Structure

### Section 1 — Hook
CLAUDE.md works. But as your setup grows — more tools, more apps, a bigger team — the config that worked for one project needs to scale. Two problems surface: you're locked to one tool, and a single file can't cover a repo with multiple distinct applications.

### Section 2 — Portability: CLAUDE.md vs AGENTS.md
- **CLAUDE.md** = Claude Code specific. No other tool reads it.
- **AGENTS.md** = portable. A growing standard read by multiple AI assistants.
- When to choose: single tool → CLAUDE.md is fine. Multiple tools or planning to migrate → AGENTS.md is the better investment.
- Practical note: you can have both. Claude Code reads both files; AGENTS.md serves everything else.

### Section 3 — Hierarchy: the monorepo cascade
- Root file sets baseline rules for the whole repo.
- Nested files in subdirectories add or override rules for that specific app or package.
- More specific always wins.
- Example file tree showing root + two packages with their own config files.
- The shape: a cone — broad at the root, specific at the tips.

### Section 4 — Putting it together
Brief practical example combining both concepts: AGENTS.md at root for portability, nested files per app for specificity. Shown as a file tree with one-line descriptions of what each file covers.

### Section 5 — What's Next / Further Reading
Links to relevant docs for AGENTS.md standard and Claude Code's configuration documentation.

---

## Tone and style

Match existing lesson style: direct, short paragraphs, no hedging. Real file tree examples over abstract description. Keep it simple — this is an introduction to advanced config, not a complete reference.

---

## Scope

Covers exactly two topics: portability (CLAUDE.md vs AGENTS.md) and hierarchy (monorepo cascade). No other advanced configuration topics. Designed to be expanded in future lessons.
