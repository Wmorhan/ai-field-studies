# What AI Knows (and Doesn't)

Before you write a single prompt, it's worth understanding what your AI assistant actually knows — and where its knowledge stops cold.

## The training cutoff

Every AI model is trained on data up to a specific date. Before that date: broad knowledge of languages, frameworks, APIs, patterns. After it: nothing.

Not "less accurate." Not "somewhat outdated." Nothing.

The model doesn't know what it doesn't know. If a major library released a breaking change six months after its training cutoff, the AI will teach you the old API — correctly, confidently, and completely wrong for your version. It won't warn you. It won't hedge. It will just be wrong.

This is the first thing to internalize: **the AI's confidence is not a reliability signal.**

## Dealing with the cutoff: live data

The fix is straightforward: inject current information at query time.

MCP (Model Context Protocol) tools can fetch live documentation and feed it directly into the AI's context before it answers. [Context7](https://context7.com) does this for library docs — when you ask about a framework's configuration, it pulls the current documentation rather than relying on the model's frozen snapshot.

**Practical example:** ask an AI (without live data) how to configure a popular framework that changed its config format in a recent major release. It will show you the old format with full confidence. Add Context7, ask the same question — it fetches the current docs and answers correctly.

This is not magic. It's giving the AI better inputs. The model's reasoning is fine; the data it had was stale.

## What the AI never knew: you

The training cutoff explains what the AI stopped learning. There's a second gap that has nothing to do with time: the AI has never known anything about you.

Not your preferred programming language. Not your team's naming conventions. Not your architectural patterns. Not how you structure a module, comment a function, or organize a test suite.

These things were never in the training data, because they're yours.

The result: generic code. Functional, often well-structured — but written in the AI's style, not yours. If you've watched a YouTube tutorial where someone pastes a prompt and gets instant working code, you've seen this. The code works. Under the hood, you'd never recognize it as yours. Different naming, different patterns, different instincts.

This isn't a flaw. The AI is a capable junior who just walked through the door. It defaults to what it was trained on — broad, general, and nothing to do with your codebase.

Capable junior. Blank slate. Needs onboarding.

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
