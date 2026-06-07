# Design: What AI Knows (and Doesn't)

**Date:** 2026-06-07  
**Output file:** `lessons/01-getting-started/what-ai-knows.md`  
**Role:** Introduction to `configure-claude-md.md` — establishes the mental model for why configuration matters

---

## Purpose

Readers coming to AI-assisted coding often trust the AI's confidence too much. This lesson corrects that by naming two hard limits on what AI knows, and connecting each limit to a concrete mitigation. It sets up the CLAUDE.md lesson by making the reader feel the conventions gap before they're taught to fix it.

---

## Structure

### Section 1 — The hook
AI writes fluent code in any language, explains frameworks, suggests patterns. That confidence is real — but it masks two hard limits. Understanding them changes how you work.

### Section 2 — The training cutoff
Every model has a cutoff date. Before it: broad knowledge of languages, frameworks, patterns. After it: nothing — no new library versions, no breaking API changes, no framework shifts since then.

The model doesn't know what it doesn't know. It answers with full confidence using whatever it last saw. A library that released a major version six months after the cutoff will be taught the old way, correctly and convincingly.

Key point: the cutoff is not obvious. The AI won't say "I'm not sure about this version." It will just be wrong.

### Section 3 — Mitigating the cutoff: live data
The fix is injecting current information at query time. MCP tools like Context7 fetch live documentation so the AI answers against the real current state — not a frozen snapshot. Brief treatment: explain the concept, name the tool, show why it matters with a concrete example (e.g. asking about a config option that changed in a recent release).

### Section 4 — What AI never knew: you
Separate problem, different cause. No amount of training covers your conventions, your preferred language, your architectural patterns, your commenting style. These were never in the training data because they're yours.

The YouTube example: you find a working solution, hand it to your AI, get working code — that looks nothing like your codebase. The AI is a capable junior who just walked in the door. It defaults to generic. It will use whatever language, style, and structure feels natural to it unless you tell it otherwise.

This is not a bug. It's just a blank slate.

### Section 5 — Bridge to configure-claude-md
Two gaps, two fixes:
- Cutoff gap → live data tools (MCP, Context7)
- Conventions gap → you have to tell it

The next lesson covers how to do that.

---

## Tone and style

Match the existing lesson style: direct, opinionated, practical. Short paragraphs. Real examples over abstract explanations. No hedging. The YouTube example and the "confident but wrong" framing are load-bearing — keep them.

---

## What this lesson does NOT cover

- Deep technical explanation of how training works
- Full MCP setup guide (that belongs elsewhere)
- All possible mitigation strategies — keep it to the two named here
