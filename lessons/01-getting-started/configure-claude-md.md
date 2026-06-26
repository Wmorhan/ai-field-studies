# Configuring AI Agents: Setting Behavior Before You Code

> **Before this lesson:** If you haven't read [What AI Knows (and Doesn't)](what-ai-knows.md), start there — it explains why this configuration matters.

## What We Learned

We made the mistake of jumping straight into using AI without setting any guardrails on how it behaves. What we got back was technically functional but full of patterns we didn't want — over-engineered solutions, unnecessary abstractions, changes to code we hadn't touched in the task. Every correction meant another iteration, which costs time and money.

What helped: configuring the AI's behavior before the session starts. Without explicit guidance, AI tools drift toward patterns that seem helpful but create problems:

- **Over-engineering** — adding abstractions and "flexibility" nobody asked for
- **Scope creep** — "improving" adjacent code while fixing something else
- **Assumption blindness** — silently picking one interpretation when requirements are unclear
- **Vague execution** — starting work without clear success criteria

Every unnecessary iteration burns time and, if you're on usage-based pricing, money. Getting configuration right early pays off quickly.

This lesson focuses on `CLAUDE.md` (used by Claude Code, Cursor, and other tools), but the principles apply to any AI assistant's configuration system — whether it's `.cursorrules`, `.aiderules`, custom system prompts, or tool-specific settings.

## Where to Put It

Claude Code reads `CLAUDE.md` files from two locations:

1. **`~/.claude/CLAUDE.md`** — Global rules that apply across all projects
2. **`<project>/.claude/CLAUDE.md`** — Project-specific rules (takes precedence over global)

We found that relying only on global rules wasn't enough. Each project has its own constraints and patterns that global rules can't cover:
- A legacy system needs different guidance than a greenfield project
- A TypeScript API has different testing patterns than a Python data pipeline
- A public-facing product has different documentation standards than an internal tool

The gap between "what the global config says" and "what this specific project actually needs" is where the AI has to guess. Five minutes writing a project-specific `CLAUDE.md` closed that gap and reduced back-and-forth significantly.

Start with global rules that reflect your general approach, then add project-specific rules that cover what makes each codebase unique.

## What to Include

Here are five principles we settled on, with examples of how we wrote them:

### 1. Think Before Coding

AI tools are biased toward action. We found that asking explicitly for clarification before execution made a real difference.

```markdown
## Think Before Coding

Don't assume. Don't hide confusion. Surface tradeoffs.

- State assumptions explicitly — If uncertain, ask rather than guess
- Present multiple interpretations — Don't pick silently when ambiguity exists
- Push back when warranted — If a simpler approach exists, say so
- Stop when confused — Name what's unclear and ask for clarification
```

### 2. Simplicity First

The AI's instinct is to add "just in case" code. We had to tell it not to.

```markdown
## Simplicity First

Minimum code that solves the problem. Nothing speculative.

- No features beyond what was asked
- No abstractions for single-use code
- No "flexibility" or "configurability" that wasn't requested
- No error handling for impossible scenarios
- If 200 lines could be 50, rewrite it
```

### 3. Surgical Changes

One thing that frustrated us early on: asking for a bug fix and getting back a refactored module. The AI was trying to help. We needed to be explicit.

```markdown
## Surgical Changes

Touch only what you must. Clean up only your own mess.

- Don't "improve" adjacent code, comments, or formatting
- Don't refactor things that aren't broken
- Match existing style, even if you'd do it differently
- If you notice unrelated dead code, mention it — don't delete it

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused
- Don't remove pre-existing dead code unless asked

The test: Every changed line should trace directly to the user's request.
```

### 4. Goal-Driven Execution

Vague tasks produce vague output. We started framing everything as a verifiable goal.

```markdown
## Goal-Driven Execution

Define success criteria. Loop until verified.

Transform imperative tasks into verifiable goals:

Instead of...          Transform to...
"Add validation"       "Write tests for invalid inputs, then make them pass"
"Fix the bug"          "Write a test that reproduces it, then make it pass"
"Refactor X"           "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

### 5. Demand Clarity

We learned to ask the AI to push back on us when we were being vague — rather than finding out three iterations later.

```markdown
## Demand Clarity

Interrogate vague requests. Don't code until requirements are unambiguous.

When a request is unclear, stop and ask:
- What's the specific scope? (which files, components, fields)
- What's the exact behavior? (steps, inputs, outputs)
- What are the edge cases? (empty, error, boundary conditions)
- What's the success criteria? (how do we know it's done right)
- Where does it integrate? (existing code, dependencies, side effects)

Red flags: "fix", "improve", "handle", "add" without specifics
The test: Could another developer implement this without asking questions?
```

## A Complete Example

Here's a global configuration that pulls these five principles together:

```markdown
# Global rules and settings for Claude

1. Think Before Coding

Don't assume. Don't hide confusion. Surface tradeoffs.

State assumptions explicitly — If uncertain, ask rather than guess
Present multiple interpretations — Don't pick silently when ambiguity exists
Push back when warranted — If a simpler approach exists, say so
Stop when confused — Name what's unclear and ask for clarification

2. Simplicity First

Minimum code that solves the problem. Nothing speculative.

No features beyond what was asked
No abstractions for single-use code
No "flexibility" or "configurability" that wasn't requested
No error handling for impossible scenarios
If 200 lines could be 50, rewrite it

3. Surgical Changes

Touch only what you must. Clean up only your own mess.

Don't "improve" adjacent code, comments, or formatting
Don't refactor things that aren't broken
Match existing style, even if you'd do it differently
If you notice unrelated dead code, mention it — don't delete it

When your changes create orphans:

    Remove imports/variables/functions that YOUR changes made unused
    Don't remove pre-existing dead code unless asked

The test: Every changed line should trace directly to the user's request.

4. Goal-Driven Execution

Define success criteria. Loop until verified.

Transform imperative tasks into verifiable goals:
Instead of...          Transform to...
"Add validation"       "Write tests for invalid inputs, then make them pass"
"Fix the bug"          "Write a test that reproduces it, then make it pass"
"Refactor X"           "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:

1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]

5. Demand Clarity

Interrogate vague requests. Don't code until requirements are unambiguous.

When a request is unclear, stop and ask:
- What's the specific scope? (which files, components, fields)
- What's the exact behavior? (steps, inputs, outputs)
- What are the edge cases? (empty, error, boundary conditions)
- What's the success criteria? (how do we know it's done right)
- Where does it integrate? (existing code, dependencies, side effects)

Red flags: "fix", "improve", "handle", "add" without specifics
The test: Could another developer implement this without asking questions?
```

## What We Took Away

1. **Configure before you code** — the AI's default behaviour is not calibrated to your project
2. **Be explicit** — vague guidance produces vague results; the AI follows instructions literally
3. **Start global, refine per project** — general philosophy at the global level, specific conventions per project
4. **Iterate on the config** — when the AI keeps doing something you don't want, add a rule; the config evolves
5. **Keep it readable** — you'll reference it when debugging unexpected AI behaviour

## What's Next

With a `CLAUDE.md` in place, the AI has something real to work from. The next lesson covers how to give it the context it needs around intent and architecture.

## Further Reading

- [Claude Code Documentation: CLAUDE.md files](https://docs.claude.ai/code)
- [Prompt Engineering Guide](https://www.promptingguide.ai/)
