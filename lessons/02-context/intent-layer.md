# The Intent Layer: Documentation That Keeps AI on Track

> **Before this lesson:** Read [Before Everything Starts](../Before%20everything%20starts.md) — it covers the shift in roles that makes this documentation necessary.

## Why This Matters

When an AI coding agent doesn't know why you're building something, it doesn't stop and ask. It guesses — and then proceeds confidently in the wrong direction.

This is the core danger of underdocumented AI-assisted development. The agent sees your codebase as a puzzle to solve on its own terms. It optimizes for code-level coherence: clean patterns, consistent naming, logical structure. But "logical" according to what goal?

Three hours later you have beautifully written code that solves the wrong problem. No warning signs. No moment where the agent flagged uncertainty. Just confident execution of a wrong assumption.

The fix isn't a better prompt. It's documentation that exists *before* the session starts — documentation that gives the agent something to check its decisions against beyond the code itself.

## The Two Layers

Every project needs coverage across two dimensions:

**The Why layer — business documentation**
What problem are we solving? For whom? What does success look like? What constraints are non-negotiable? What have we explicitly decided *not* to do?

**The How layer — architecture documentation**
What technical choices were made? What patterns do we follow? What did we decide against, and why? How does the system fit together?

The naming doesn't matter. Call them `business.md` and `architecture.md`, or `goals.md` and `design.md`, or anything else. What matters is *coverage* — that both dimensions exist and are written down.

The gray zone between them is real and fine. "We chose a monorepo because the teams need to stay aligned" sits in both. Don't spend time debating taxonomy. Spend it writing content.

**One without the other is still a guess:**

- *How without why:* The agent knows you're using microservices but not why. It suggests consolidating them to reduce complexity — technically reasonable, strategically wrong.
- *Why without how:* The agent knows you want fast iteration but not your architecture constraints. It suggests shortcuts that violate the patterns you've deliberately built.

Both layers together create an anchor strong enough to hold.

## Essence Precedes Existence

Write the why before the how.

The architecture is a consequence of the business intent — not the other way around. You don't pick a database before you know what you're storing or why. You don't choose a service boundary before you understand the business domain it represents.

In traditional development, skipping this step is a bad habit. In AI-assisted development, it's a structural failure. The agent will fill in missing intent with assumptions. Those assumptions will be internally consistent and confidently executed. You won't know they were wrong until the consequences show up.

The why document is the foundation. Build architecture on top of it.

## What to Write

### Business documentation

This is the *why*. Keep it direct and opinionated — vague goals produce vague code.

```
# Project: [Name]

## Problem
[One paragraph. What situation is broken or missing? Who feels it?]

## Goal
[What does this project achieve when done? Specific and measurable if possible.]

## Users
[Who uses this? What do they need? What do they not care about?]

## Constraints
[What is non-negotiable? Budget, timeline, compliance, existing systems.]

## Out of scope
[What are we explicitly not building? This is as important as what we are building.]

## Success criteria
[How do we know this worked?]
```

### Architecture documentation

This is the *how*. Focus on decisions and their reasoning — not just what was chosen, but what was considered and rejected.

```
# Architecture: [Name]

## Overview
[One paragraph describing the system shape.]

## Key decisions
- [Decision]: [What we chose] — [Why]
- [Decision]: [What we chose] — [Why, and what we rejected]

## Patterns we follow
[Naming, structure, testing, error handling conventions.]

## Patterns we avoid
[Anti-patterns specific to this project and why.]

## Dependencies and integrations
[External systems, APIs, libraries this project relies on.]
```

### Example folder structure

```
docs/
  business.md       # the why
  architecture.md   # the how
  decisions/        # optional: individual decision records for major choices
    001-database.md
    002-auth.md
```

This doesn't need to be elaborate. Two files — one for why, one for how — is enough to give an AI agent a real anchor. Start there.

## Writing for an AI Reader

Documentation for AI agents is different from documentation for humans.

When you write for a human reader, you compress. You assume shared context, skip obvious things, and trust that a colleague will read between the lines. With AI you cannot do this — the agent has no shared context, makes no inferences, and will fill any gap with a guess.

Write explicitly. State conclusions directly, not just the reasoning trail that leads to them. Avoid phrases like "as discussed" or "per the original design" — the agent has no memory of those conversations. If something is important, say it outright.

**There is no "too much information" here.** An AI agent reads thousands of words in seconds with no cognitive fatigue. The instinct to trim documentation to avoid overwhelming a reader does not apply. Err heavily on the side of more: more context, more reasoning, more explicit statements of what might seem obvious. A well-documented why and how cannot be too long — it can only be incomplete.

This is a genuine inversion of normal documentation instincts. Write as if your reader is fast, tireless, and has no prior knowledge of your project. That reader will use everything you give it.

**Content is king.** Adding information is more important than formatting it. A wall of plain text that covers the why and the how thoroughly will serve your agent better than a beautifully structured document with gaps. Don't let the pursuit of clean formatting slow down or replace the act of writing. Get the content down first — structure it later if at all.

## Making It Stick

Writing the documentation is step one. Ensuring the agent reads it is step two.

**Reference it in your CLAUDE.md:**

```markdown
## Project context
Before starting any task, read:
- docs/business.md — project goals and constraints
- docs/architecture.md — technical decisions and patterns

Do not make architectural decisions that contradict these documents.
If a task seems to conflict with them, stop and ask.
```

This makes reading the intent layer a default behavior, not something you remember to ask for.

**Treat it as a session anchor, not a one-time setup.** At the start of a new session, on a complex task, or when something feels off — point the agent back to the docs explicitly. The context window is finite. A long session will drift without re-grounding.

**Memory plugins help, but don't replace this.** Tools that persist state across sessions (memory plugins, vector stores, project memory) capture *what happened* — they don't capture *why you made the choices you made*. Deep documentation is still necessary. Memory plugins give the agent access to history; your docs give it access to intent.

**Update the docs as the project evolves.** An outdated why document is worse than none — the agent will follow it confidently in the wrong direction. When a business goal changes, update the doc before the next session.

## Key Takeaways

1. **AI agents fill intent gaps with guesses** — and they do it silently and confidently
2. **Two layers are required** — why (business) and how (architecture); one without the other is incomplete
3. **Essence precedes existence** — write the why before the how, because the how follows from it
4. **Coverage matters more than structure** — the format is flexible; the content is not optional
5. **Wire it into your workflow** — reference docs in CLAUDE.md, re-read at session start, update when goals change

## What's Next

With intent documentation in place, the agent has something real to navigate by. The next lesson covers prompt patterns — how to communicate tasks in ways that produce precise, predictable results.

## Further Reading

- [Architectural Decision Records (ADRs)](https://adr.github.io/) — a lightweight format for documenting technical decisions
- [C4 Model](https://c4model.com/) — a structured approach to architecture documentation at different levels of detail
