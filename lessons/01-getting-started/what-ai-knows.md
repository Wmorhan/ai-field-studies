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
