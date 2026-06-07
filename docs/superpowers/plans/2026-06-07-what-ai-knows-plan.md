# What AI Knows Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Write `lessons/01-getting-started/what-ai-knows.md` — a focused lesson that establishes the mental model for AI's knowledge limits before the reader reaches the CLAUDE.md configuration lesson.

**Architecture:** Single new markdown file covering two gaps (training cutoff, conventions) and two mitigations (live data tools, CLAUDE.md). Ends with a bridge into `configure-claude-md.md`. Small addition to `configure-claude-md.md` to reference this as prerequisite reading.

**Tech Stack:** Markdown. No code, no tooling. Verify by reading for tone consistency with `configure-claude-md.md`.

---

### Task 1: Hook and training cutoff section

**Files:**
- Create: `lessons/01-getting-started/what-ai-knows.md`
- Reference: `lessons/01-getting-started/configure-claude-md.md` (for tone matching)

- [ ] **Step 1: Create the file with the hook and training cutoff section**

Write the following content to `lessons/01-getting-started/what-ai-knows.md`:

```markdown
# What AI Knows (and Doesn't)

Before you write a single prompt, it's worth understanding what your AI assistant actually knows — and where its knowledge stops cold.

## The training cutoff

Every AI model is trained on data up to a specific date. Before that date: broad knowledge of languages, frameworks, APIs, patterns. After it: nothing.

Not "less accurate." Not "somewhat outdated." Nothing.

The model doesn't know what it doesn't know. If a major library released a breaking change six months after its training cutoff, the AI will teach you the old API — correctly, confidently, and completely wrong for your version. It won't warn you. It won't hedge. It will just be wrong.

This is the first thing to internalize: **the AI's confidence is not a reliability signal.**
```

- [ ] **Step 2: Verify tone against existing lesson**

Read the opening of `lessons/01-getting-started/configure-claude-md.md`. Check: short paragraphs, direct statements, no hedging, bold used for key points. Adjust if needed.

- [ ] **Step 3: Commit**

```bash
git add lessons/01-getting-started/what-ai-knows.md
git commit -m "Add what-ai-knows lesson: hook and training cutoff section"
```

---

### Task 2: Live data mitigation section

**Files:**
- Modify: `lessons/01-getting-started/what-ai-knows.md`

- [ ] **Step 1: Append the live data section**

Append to `lessons/01-getting-started/what-ai-knows.md`:

```markdown

## Dealing with the cutoff: live data

The fix is straightforward: inject current information at query time.

MCP (Model Context Protocol) tools can fetch live documentation and feed it directly into the AI's context before it answers. [Context7](https://context7.com) does this for library docs — when you ask about a framework's configuration, it pulls the current documentation rather than relying on the model's frozen snapshot.

**Practical example:** ask an AI (without live data) how to configure a popular framework that changed its config format in a recent major release. It will show you the old format with full confidence. Add Context7, ask the same question — it fetches the current docs and answers correctly.

This is not magic. It's giving the AI better inputs. The model's reasoning is fine; the data it had was stale.
```

- [ ] **Step 2: Check the Context7 link is correct**

The URL `https://context7.com` should resolve to the Context7 product page. If it doesn't, use `https://github.com/upstash/context7` as the fallback.

- [ ] **Step 3: Commit**

```bash
git add lessons/01-getting-started/what-ai-knows.md
git commit -m "Add what-ai-knows lesson: live data mitigation section"
```

---

### Task 3: Conventions gap section

**Files:**
- Modify: `lessons/01-getting-started/what-ai-knows.md`

- [ ] **Step 1: Append the conventions gap section**

Append to `lessons/01-getting-started/what-ai-knows.md`:

```markdown

## What the AI never knew: you

The training cutoff explains what the AI stopped learning. There's a second gap that has nothing to do with time: the AI has never known anything about you.

Not your preferred programming language. Not your team's naming conventions. Not your architectural patterns. Not how you structure a module, comment a function, or organize a test suite.

These things were never in the training data, because they're yours.

The result: generic code. Functional, often well-structured — but written in the AI's style, not yours. If you've watched a YouTube tutorial where someone pastes a prompt and gets instant working code, you've seen this. The code works. Under the hood, you'd never recognize it as yours. Different naming, different patterns, different instincts.

This isn't a flaw. The AI is a capable junior who just walked through the door. It defaults to what it was trained on — broad, general, and nothing to do with your codebase.

Capable junior. Blank slate. Needs onboarding.
```

- [ ] **Step 2: Verify the YouTube example lands clearly**

Re-read from the top of the file. The "capable junior" framing should feel like the natural conclusion of the section, not a sudden shift. Adjust the final two sentences if the landing feels abrupt.

- [ ] **Step 3: Commit**

```bash
git add lessons/01-getting-started/what-ai-knows.md
git commit -m "Add what-ai-knows lesson: conventions gap section"
```

---

### Task 4: Bridge, What's Next, and Further Reading

**Files:**
- Modify: `lessons/01-getting-started/what-ai-knows.md`

- [ ] **Step 1: Append the bridge and closing sections**

Append to `lessons/01-getting-started/what-ai-knows.md`:

```markdown

## Two gaps, two fixes

So you're working with an assistant that:
- Knows nothing that happened after its training cutoff
- Knows nothing about you, your conventions, or your codebase

Both are solvable. Both require you to take action.

**Cutoff gap** → feed it current information. MCP tools like Context7 handle library docs automatically. For domain-specific context, paste in what it needs.

**Conventions gap** → tell it who you are and how you work. That's what the next lesson covers.

## What's Next

[Configuring AI Agents: Setting Behavior Before You Code](configure-claude-md.md) — how to write a `CLAUDE.md` that teaches the AI your conventions before you start.

## Further Reading

- [Model Context Protocol (MCP)](https://modelcontextprotocol.io) — the open standard for connecting AI to live data sources
- [Context7](https://context7.com) — live documentation injection for AI assistants
```

- [ ] **Step 2: Read the full file top to bottom**

Check: does it flow? Does the bridge section feel like a natural summary rather than a tacked-on ending? Does "What's Next" connect cleanly to the actual content of `configure-claude-md.md`?

- [ ] **Step 3: Commit**

```bash
git add lessons/01-getting-started/what-ai-knows.md
git commit -m "Add what-ai-knows lesson: bridge and closing sections"
```

---

### Task 5: Link from configure-claude-md.md

**Files:**
- Modify: `lessons/01-getting-started/configure-claude-md.md`

- [ ] **Step 1: Add prerequisite reference at top of configure-claude-md.md**

After the `# Configuring AI Agents: Setting Behavior Before You Code` heading and before `## Why This Matters`, insert:

```markdown
> **Before this lesson:** If you haven't read [What AI Knows (and Doesn't)](what-ai-knows.md), start there — it explains why this configuration matters.

```

- [ ] **Step 2: Verify it reads naturally**

Read the opening of `configure-claude-md.md` with the new line in place. The callout should feel like a helpful pointer, not a prerequisite gate. If it feels too heavy, reduce to a single inline sentence at the start of `## Why This Matters`.

- [ ] **Step 3: Commit**

```bash
git add lessons/01-getting-started/configure-claude-md.md
git commit -m "Link what-ai-knows as prerequisite reading in configure-claude-md"
```
