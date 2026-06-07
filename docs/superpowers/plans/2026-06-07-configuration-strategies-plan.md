# Configuration Strategies Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Write `lessons/05-advanced/configuration-strategies.md` — an advanced lesson covering tool portability (CLAUDE.md vs AGENTS.md) and monorepo hierarchical configuration.

**Architecture:** Single markdown file with five sections following the "scaling your configuration" narrative. No code, no tooling. Prerequisite: reader has completed `lessons/01-getting-started/configure-claude-md.md`.

**Tech Stack:** Markdown. Verify by reading for tone consistency with `configure-claude-md.md` and internal logic of file tree examples.

---

### Task 1: Hook and file scaffold

**Files:**
- Create: `lessons/05-advanced/configuration-strategies.md`
- Reference: `lessons/01-getting-started/configure-claude-md.md` (tone matching)

- [ ] **Step 1: Create the file with the hook section**

Write the following to `lessons/05-advanced/configuration-strategies.md`:

```markdown
# Scaling Your Configuration

> **Prerequisite:** This lesson assumes you've completed [Configuring AI Agents: Setting Behavior Before You Code](../01-getting-started/configure-claude-md.md).

CLAUDE.md works. But as your setup grows — more tools, more apps, a bigger team — the config that worked for one project needs to scale.

Two problems surface:

- You're locked to one tool. CLAUDE.md only works with Claude Code.
- A single file can't cover a monorepo where different apps have different conventions.

This lesson gives the practical fix for both.
```

- [ ] **Step 2: Verify tone**

Read the opening of `configure-claude-md.md`. Check: short paragraphs, direct statements, no hedging, problems named before solutions. Adjust if needed.

- [ ] **Step 3: Commit**

```bash
git add lessons/05-advanced/configuration-strategies.md
git commit -m "Add configuration-strategies lesson: scaffold and hook"
```

---

### Task 2: Portability section (CLAUDE.md vs AGENTS.md)

**Files:**
- Modify: `lessons/05-advanced/configuration-strategies.md`

- [ ] **Step 1: Append the portability section**

Append to `lessons/05-advanced/configuration-strategies.md`:

```markdown

## Tool portability: CLAUDE.md vs AGENTS.md

`CLAUDE.md` is Claude Code specific. No other AI assistant reads it.

`AGENTS.md` is the portable alternative — a growing standard read by multiple AI assistants. If you work with more than one tool, or want the option to migrate later, `AGENTS.md` is the better investment.

The practical rule:

- **Single tool, single team** → `CLAUDE.md` is fine
- **Multiple tools, or planning to migrate** → use `AGENTS.md`

You can have both. Claude Code reads both files — `AGENTS.md` serves everything else. If you're starting fresh and unsure, default to `AGENTS.md`.
```

- [ ] **Step 2: Verify the rule is crisp**

Re-read the section. The two-bullet decision rule should be scannable in under five seconds. If it requires more than one read to understand, simplify.

- [ ] **Step 3: Commit**

```bash
git add lessons/05-advanced/configuration-strategies.md
git commit -m "Add configuration-strategies lesson: portability section"
```

---

### Task 3: Monorepo hierarchy section

**Files:**
- Modify: `lessons/05-advanced/configuration-strategies.md`

- [ ] **Step 1: Append the hierarchy section**

Append to `lessons/05-advanced/configuration-strategies.md`:

```markdown

## Hierarchy: configuring a monorepo

A single config file at the root sets baseline rules for the whole repo. Nested config files in subdirectories add or override rules for that specific app or package. More specific always wins.

```
my-monorepo/
├── AGENTS.md          ← baseline: language, general conventions
├── packages/
│   ├── api/
│   │   └── AGENTS.md  ← API-specific: Node.js patterns, REST conventions
│   └── web/
│       └── AGENTS.md  ← frontend-specific: React patterns, CSS conventions
```

Think of it as a cone: broad rules at the root, specific rules at the tips. Each nested file only needs to cover what's different — the root rules still apply unless overridden.
```

- [ ] **Step 2: Verify the file tree renders correctly**

Check that the triple-backtick code block for the file tree is properly closed and the indentation is consistent. The tree should be immediately readable.

- [ ] **Step 3: Commit**

```bash
git add lessons/05-advanced/configuration-strategies.md
git commit -m "Add configuration-strategies lesson: monorepo hierarchy section"
```

---

### Task 4: Putting it together and closing sections

**Files:**
- Modify: `lessons/05-advanced/configuration-strategies.md`

- [ ] **Step 1: Append the summary and closing sections**

Append to `lessons/05-advanced/configuration-strategies.md`:

```markdown

## Putting it together

A practical starting point for a multi-app monorepo:

```
my-monorepo/
├── AGENTS.md          ← portable baseline, read by all tools
├── .claude/
│   └── CLAUDE.md      ← Claude-specific behavior (optional)
├── packages/
│   ├── api/
│   │   └── AGENTS.md  ← overrides and additions for the API package
│   └── web/
│       └── AGENTS.md  ← overrides and additions for the web package
```

Root `AGENTS.md` carries your general conventions. Package-level files only need to cover what's different. Claude-specific behavior (like tool permissions or memory settings) stays in `.claude/CLAUDE.md` where only Claude Code will find it.

## What's Next

Explore other advanced patterns in the `lessons/05-advanced/` directory.

## Further Reading

- [AGENTS.md standard](https://github.com/anthropics/anthropic-quickstarts) — background on the portable configuration standard
- [Claude Code: CLAUDE.md documentation](https://docs.anthropic.com/en/docs/claude-code/memory) — full reference for Claude-specific configuration
```

- [ ] **Step 2: Read the full lesson top to bottom**

Check: does the narrative hold together? Hook → portability decision → hierarchy pattern → combined example. Each section should feel like it earns the next. Adjust any transition that feels abrupt.

- [ ] **Step 3: Commit**

```bash
git add lessons/05-advanced/configuration-strategies.md
git commit -m "Add configuration-strategies lesson: summary and closing sections"
```
