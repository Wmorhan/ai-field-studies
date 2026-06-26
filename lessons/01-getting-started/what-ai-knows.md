# What AI Knows (and Doesn't)

One of the first things we had to get our heads around was the gap between what AI confidently tells you and what it actually knows. Getting this wrong early on cost us time we didn't expect to lose.

## The training cutoff

Every AI model is trained on data up to a specific date. Before that date: broad knowledge of languages, frameworks, APIs, patterns. After it: nothing.

Not "less accurate." Not "somewhat outdated." Nothing.

The model doesn't know what it doesn't know. If a major library released a breaking change six months after its training cutoff, the AI will walk you through the old approach — correctly, confidently, and completely wrong for your version. It won't warn you. It won't hedge. It will just be wrong.

This is the first thing we learned to keep in mind: **the AI's confidence is not a reliability signal.**

## Dealing with the cutoff: live data

The fix is straightforward: give it current information at the moment you ask.

MCP tools (Model Context Protocol — the standard for connecting AI to live data sources) can fetch up-to-date documentation and feed it directly into the AI's context before it answers. [Context7](https://context7.com) does this for library docs — when you ask about a framework's configuration, it pulls the current documentation rather than relying on the model's frozen snapshot.

**A concrete example we ran into:** ask an AI about configuring a popular framework that changed its config format in a recent major release. Without live data, it shows you the old format with full confidence. Add Context7, ask the same question — it fetches the current docs and answers correctly.

This isn't magic. We're giving the AI better inputs. The model's reasoning is sound; the data it had was just stale.

## What the AI never knew: you

The training cutoff explains what the AI stopped learning. There's a second gap that has nothing to do with time: the AI has never known anything about your organisation, your team, or your way of working.

Not your preferred languages. Not your naming conventions. Not your architectural patterns. Not how you structure a module, comment a function, or organise tests.

These things were never in the training data, because they're yours.

The result: generic output. Functional, often well-structured — but written in the AI's style, not yours. We noticed this early on when the code that came back worked fine but looked nothing like what our teams would write. Different naming, different patterns, different instincts.

This isn't a flaw. The AI is like a capable new joiner who just walked through the door. It defaults to what it was trained on — broad, general, and nothing specific to your context.

Capable. Blank slate. Needs onboarding.

## Two gaps, two fixes

What we were dealing with:
- An assistant that knows nothing after its training cutoff
- An assistant that knows nothing about how we work

Both are solvable. Both require us to take action.

**Cutoff gap** → feed it current information. MCP tools like Context7 handle library docs automatically. For domain-specific context, provide it directly.

**Conventions gap** → tell it who you are and how you work. That's what the next lesson covers.

## What's Next

[Configuring AI Agents: Setting Behavior Before You Code](configure-claude-md.md) — how to write a `CLAUDE.md` that teaches the AI your conventions before a session starts.

## Further Reading

- [Model Context Protocol (MCP)](https://modelcontextprotocol.io) — the open standard for connecting AI to live data sources
- [Context7](https://context7.com) — live documentation injection for AI assistants
