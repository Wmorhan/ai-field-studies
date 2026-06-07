# Scaling Your Configuration

> **Prerequisite:** This lesson assumes you've completed [Configuring AI Agents: Setting Behavior Before You Code](../01-getting-started/configure-claude-md.md).

CLAUDE.md works. But as your setup grows — more tools, more apps, a bigger team — the config that worked for one project needs to scale.

Two problems surface:

- You're locked to one tool. CLAUDE.md only works with Claude Code.
- A single file can't cover a monorepo where different apps have different conventions.

This lesson gives the practical fix for both.

## Tool portability: CLAUDE.md vs AGENTS.md

`CLAUDE.md` is Claude Code specific. No other AI assistant reads it.

`AGENTS.md` is the portable alternative — a growing standard read by multiple AI assistants. If you work with more than one tool, or want the option to migrate later, `AGENTS.md` is the better investment.

The practical rule:

- **Single tool, single team** → `CLAUDE.md` is fine
- **Multiple tools, or planning to migrate** → use `AGENTS.md`

You can have both. Claude Code reads both files — `AGENTS.md` serves everything else. If you're starting fresh and unsure, default to `AGENTS.md`.

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
