# Configuring AI Agents: Setting Behavior Before You Code

## Why This Matters

Before writing a single line of code with an AI assistant, you should configure how it behaves. Without guidance, AI tools often fall into patterns that seem helpful but create problems:

- **Over-engineering** - Adding abstractions, configuration layers, and "flexibility" you didn't ask for
- **Scope creep** - "Improving" adjacent code while fixing a bug
- **Assumption blindness** - Silently picking one interpretation when requirements are unclear
- **Vague execution** - Starting work without clear success criteria

**These patterns waste tokens, which costs you money.** Every unnecessary iteration, every over-engineered solution, every misunderstood requirement burns through your API budget or subscription limits. Proper configuration pays for itself immediately.

This lesson focuses on `CLAUDE.md` (used by Claude Code, Cursor, and other tools), but the principles apply to any AI coding assistant's configuration system - whether it's `.cursorrules`, `.aiderules`, custom system prompts, or tool-specific settings.

## Where to Put It

Claude Code reads `CLAUDE.md` files from two locations:

1. **`~/.claude/CLAUDE.md`** - Global rules for all projects
2. **`<project>/.claude/CLAUDE.md`** - Project-specific rules (overrides global)

**Don't be lazy here.** A root configuration is a starting point, not a solution. Each project has unique constraints:
- A legacy monolith needs different refactoring rules than a greenfield microservice
- A TypeScript API has different testing patterns than a Python data pipeline
- A public library requires different documentation standards than an internal tool

**Laziness costs money.** Relying solely on global rules means the AI doesn't know your project's specific conventions, tech stack quirks, or team preferences. It will guess, iterate, and burn tokens on work that doesn't fit. Five minutes configuring a project-specific `CLAUDE.md` saves hours of back-and-forth corrections.

Start with global rules that reflect your general coding philosophy, then **always** add project-specific rules that capture what makes this codebase unique.

## What to Include

Your `CLAUDE.md` should address the behaviors that matter most to you. Here are five core principles with real examples:

### 1. Think Before Coding

AI tools are biased toward action. Teach them to stop and clarify first.

```markdown
## Think Before Coding

Don't assume. Don't hide confusion. Surface tradeoffs.

- State assumptions explicitly — If uncertain, ask rather than guess
- Present multiple interpretations — Don't pick silently when ambiguity exists
- Push back when warranted — If a simpler approach exists, say so
- Stop when confused — Name what's unclear and ask for clarification
```

**Why this works:** Explicit instruction to pause prevents wasted work on the wrong problem.

### 2. Simplicity First

AI models love adding "just in case" code. Constrain this.

```markdown
## Simplicity First

Minimum code that solves the problem. Nothing speculative.

- No features beyond what was asked
- No abstractions for single-use code
- No "flexibility" or "configurability" that wasn't requested
- No error handling for impossible scenarios
- If 200 lines could be 50, rewrite it
```

**Why this works:** Clear constraints against over-engineering keep code maintainable.

### 3. Surgical Changes

Prevent "helpful" refactoring that wasn't requested.

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

**Why this works:** Reduces diff noise and avoids accidental breakage of working code.

### 4. Goal-Driven Execution

Transform vague requests into verifiable goals.

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

Strong success criteria let the LLM loop independently.
Weak criteria ("make it work") require constant clarification.
```

**Why this works:** Clear success criteria enable autonomous execution and reduce back-and-forth.

### 5. Demand Clarity

Force the AI to interrogate vague requests.

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

**Why this works:** Prevents wasted iterations on misunderstood requirements.

## Real Example: Complete CLAUDE.md

Here's a complete global configuration that implements all five principles:

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
Instead of... 		Transform to...
"Add validation" 	"Write tests for invalid inputs, then make them pass"
"Fix the bug" 		"Write a test that reproduces it, then make it pass"
"Refactor X" 		"Ensure tests pass before and after"

For multi-step tasks, state a brief plan:

1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]

Strong success criteria let the LLM loop independently. 
Weak criteria ("make it work") require constant clarification.

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

## Key Takeaways

1. **Configure before you code** - Don't rely on default AI behavior
2. **Be explicit** - AI tools follow instructions literally; vague guidance produces vague results
3. **Start global, refine per-project** - Common patterns go in `~/.claude/CLAUDE.md`, project quirks go in project-specific files
4. **Test and iterate** - If Claude keeps doing something you don't want, add a rule against it
5. **Keep it readable** - You'll reference this file when debugging AI behavior

## What's Next

With your `CLAUDE.md` configured, you're ready to start coding with clear behavioral expectations. The next lesson covers effective prompt patterns for common tasks.

## Further Reading

- [Claude Code Documentation: CLAUDE.md files](https://docs.claude.ai/code)
- [Prompt Engineering Guide](https://www.promptingguide.ai/)
