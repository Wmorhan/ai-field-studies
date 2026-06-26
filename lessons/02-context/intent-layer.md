# The Intent Layer: Documentation That Keeps AI on Track

> **Before this lesson:** Read [Before Everything Starts](../Before%20everything%20starts.md) — it covers the shift in roles that makes this documentation necessary.

## What We Kept Running Into

When an AI coding agent doesn't know why something is being built, it doesn't stop and ask. It guesses — and then proceeds confidently in the wrong direction.

This is the pattern that caught us out most often in early AI-assisted work. The agent sees the codebase as a puzzle to solve on its own terms. It optimises for code-level coherence: clean patterns, consistent naming, logical structure. But "logical" according to what goal?

Three hours later there's beautifully written code solving the wrong problem. No warning signs. No moment where the agent flagged uncertainty. Just confident execution of a wrong assumption.

The fix wasn't a better prompt. It was documentation that existed *before* the session started — something that gave the agent a reference point beyond the code itself.

## The Two Layers

What we found: every project needs coverage across two dimensions.

**The Why layer — business documentation**
What problem are we solving? For whom? What does success look like? What constraints are non-negotiable? What have we explicitly decided *not* to do?

**The How layer — architecture documentation**
What technical choices were made? What patterns do we follow? What did we decide against, and why? How does the system fit together?

The naming doesn't matter. Call them `business.md` and `architecture.md`, or `goals.md` and `design.md`. What matters is *coverage* — that both dimensions exist and are written down.

**One without the other is still a guess:**

- *How without why:* The agent knows the technical setup but not the reason behind it. It suggests "improvements" that are technically reasonable and strategically wrong.
- *Why without how:* The agent knows what we're trying to achieve but not the constraints we're working within. It takes shortcuts that violate the patterns we've deliberately built.

Both layers together give the agent something solid to navigate by.

## Essence Precedes Existence

Write the why before the how.

The architecture follows from the business intent — not the other way around. We noticed that when teams skipped the why document and went straight to architecture, the AI would start filling in business assumptions on its own. Those assumptions were internally consistent and confidently executed. The consequences showed up later.

The why document is the foundation. Everything else builds on top of it.

## What to Write

### Business documentation

This is the *why*. Keep it direct — vague goals produce vague output.

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

Two files is enough to make a real difference. Start there.

## Writing for an AI Reader

Something we had to unlearn: the compression instincts that work for human documentation don't work here.

When writing for a human reader, we compress. We assume shared context, skip obvious things, trust that a colleague will read between the lines. With AI we can't do this — the agent has no shared context, makes no inferences, and will fill any gap with a guess.

Write explicitly. State conclusions directly, not just the reasoning trail that leads to them. Avoid phrases like "as discussed" or "per the original design" — the agent has no memory of those conversations. If something is important, say it outright.

**There is no "too much information" here.** An AI agent reads thousands of words in seconds without fatigue. The instinct to keep documentation short doesn't apply. Err heavily on the side of more. A well-documented why and how cannot be too long — it can only be incomplete.

This was a genuine inversion for us. Write as if the reader is fast, tireless, and has no prior knowledge of the project. That reader will use everything given to it.

**Content over formatting.** A dense block of plain text that covers the why and the how thoroughly serves the agent better than a beautifully structured document with gaps. Get the content down first — structure it later if at all.

## The One Thing We Couldn't Delegate

The intent layer is the one thing an AI cannot write for itself.

An AI agent can write code, review pull requests, generate tests, refactor modules. But it cannot define its own purpose. It cannot decide what problem is worth solving, what constraints matter, or what success looks like. Those are human judgements — and without them written down, the agent operates on assumptions.

This is what we've come to see as the core responsibility in AI-assisted work. We bring the why. The agent brings the execution. If the why is missing, we haven't freed ourselves from work — we've just hidden it inside the agent's guesses, where it's invisible until something goes wrong.

Writing the intent layer is not optional overhead. It is the job.

## Making It Stick

Writing the documentation is step one. Making sure the agent reads it is step two.

**Reference it in your CLAUDE.md:**

```markdown
## Project context
Before starting any task, read:
- docs/business.md — project goals and constraints
- docs/architecture.md — technical decisions and patterns

Do not make architectural decisions that contradict these documents.
If a task seems to conflict with them, stop and ask.
```

This makes reading the intent layer a default behaviour, not something you remember to ask for.

**Treat it as a session anchor, not a one-time setup.** At the start of a new session, on a complex task, or when something feels off — point the agent back to the docs explicitly. Context windows are finite. Long sessions drift without re-grounding.

**Update the docs as the project evolves.** An outdated why document is worse than none — the agent will follow it confidently in the wrong direction. When goals change, update the doc before the next session.

## What We Took Away

1. **AI agents fill intent gaps with guesses** — and they do it silently and confidently
2. **Two layers are required** — why (business) and how (architecture); one without the other is incomplete
3. **Essence precedes existence** — write the why before the how, because the how follows from it
4. **Coverage matters more than structure** — the format is flexible; the content is not optional
5. **Wire it into your workflow** — reference docs in CLAUDE.md, re-read at session start, update when goals change

## What's Next

With intent documentation in place, the agent has something real to navigate by. The next lesson covers how to communicate individual tasks effectively — turning vague requests into precise, verifiable work.

## Further Reading

- [Architectural Decision Records (ADRs)](https://adr.github.io/) — a lightweight format for documenting technical decisions
- [C4 Model](https://c4model.com/) — a structured approach to architecture documentation at different levels of detail
