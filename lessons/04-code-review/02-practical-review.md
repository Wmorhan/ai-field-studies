# Practical Code Review: What to Look For

> **Previous:** [Code Review in the Age of AI: Don't Get Comfortable](./01-introduction.md)

## Where We Start

The intro lesson established the posture: go in assuming there are errors, and go looking for them. This lesson is about where to look.

AI-generated code has systematic blind spots — categories of mistake it makes more often, more consistently, and more invisibly than a human would. Knowing these doesn't replace judgment, but it tells you where to push hardest.

## The Two Reads

We found it helped to separate the review into two distinct passes, because they require different mental modes.

**First read: what does this actually do?**
Set aside whether it's correct. Trace what the code does, mechanically. Follow the logic. Understand the flow. Don't evaluate yet — just understand.

This matters because AI output can look correct at a glance while doing something subtly different from what was asked. You can't catch the gap between "what was requested" and "what was built" if you skip to evaluation before you've understood what was built.

**Second read: is what it does actually right?**
Now evaluate. Does this match the intent? Does it handle what it needs to handle? Where does it assume things it shouldn't? Where does the logic break?

Skipping the first read and going straight to evaluation is how plausible-looking errors get through. You're evaluating your impression of the code, not the code itself.

## Where AI Consistently Falls Short

These are the areas we learned to push hardest on.

### The edges and the unhappy paths

AI handles the happy path well. The main flow, the expected input, the successful case — these tend to be solid. What we found consistently weak: everything else.

What happens with bad input? What happens when the network call fails halfway through? What happens when two users hit this simultaneously? What happens when the database returns zero rows instead of one?

Trace the unhappy paths deliberately. Don't assume they're handled because error handling code is present — check that the error handling is *correct*. AI frequently writes try/catch blocks that catch everything and do nothing useful, or that catch too narrowly and miss the actual failure mode.

### Edge cases at the boundaries

Where does this code touch things outside itself? User input. Database queries. External APIs. File system. Those boundaries are where the most consequential errors live.

At every boundary, ask: what assumptions is this code making about what comes in? Are those assumptions validated? What happens when they're violated?

AI tends to assume clean inputs and cooperative external systems. Production doesn't provide either.

### Security at the entry points

We cover this in depth in the security lessons, but in the context of code review specifically: check every place where external data enters the system.

Is user input sanitised before it touches a database query? Are file paths validated before they're used? Are API responses treated as untrusted data before being acted on? Is anything sensitive ending up in logs?

AI code is often structurally sound and security-naive. The shape is right; the assumptions about what the environment will throw at it are not.

### The logic at the edges of conditions

Conditional logic is where subtle errors live. Off-by-one. Wrong operator (`<` vs `<=`). A condition that handles three of four cases correctly. A boolean expression that looks right but has operator precedence working against it.

We found it worth reading every condition slowly and asking: what input makes this true? What makes it false? Is that what we want?

### What the tests actually test

If AI wrote the tests alongside the code, verify that the tests are actually testing the right things. We've seen AI produce tests that pass by construction — tests that can't fail because they're not actually asserting meaningful behaviour.

The practical check: could this test pass even if the implementation was broken? If the answer is yes, the test isn't doing its job.

And run them. Tests that pass when read and fail when run reveal a different category of problem than tests that are logically wrong.

### Fit with the actual codebase

AI defaults to its training patterns — the conventions, idioms, and approaches that were most common in the data it was trained on. Those are not your conventions.

Ask: does this look like the rest of our codebase? Does it follow our naming, our error handling patterns, our layering? Does it use the abstractions we've already built, or does it reinvent them?

Code that works correctly but doesn't fit the codebase creates long-term maintenance cost. Inconsistency compounds over time.

### The problem that was actually solved

This one matters more than it sounds, and it took us a while to fully appreciate why.

AI approaches your code like a puzzle to be solved as quickly as possible. Given a task, it moves toward a working solution by the shortest available path. That's not a flaw in the model — it's how it operates. The problem is what happens when there are gaps.

Gaps in requirements. Gaps in context. Gaps between what was said and what was meant. When the AI encounters a gap, it doesn't stop and ask. It fills the gap with whatever gets to a solution fastest. Not the most architecturally sound solution. Not the solution that fits your long-term patterns. The shortest path to something that works.

This is why the intent layer — your architectural documentation, your business constraints, your explicit decisions about what this system is and isn't — matters so much in a review. If the AI wasn't given that documentation, or wasn't pointed to it, it had no anchor. It improvised. And the improvisation will be locally coherent and architecturally naive: code that solves the stated problem without regard for how that solution fits the larger system it's entering.

What we learned to check in review: not just "does this work?" but "did it take a shortcut?" Shortcuts in AI code tend to look like working solutions. They compile, they pass tests, they do the thing they were asked to do. What they skip is the constraint that wasn't in the prompt — the pattern the rest of the codebase follows, the architectural boundary that should have been respected, the non-functional requirement that wasn't stated explicitly because it seemed obvious.

Go back to the original requirement and the architectural documentation. Does this code satisfy both? Not "does it look like it satisfies them" — does it actually satisfy them, including the constraints that weren't spelled out in the task but are written down somewhere the AI wasn't told to read?

If the answer is unclear, the gap is in the documentation. Fix the documentation before approving the code.

## What Not to Let AI Review

We tried having AI review AI-generated code. The results were predictable in hindsight: it found formatting issues, variable name suggestions, and minor style observations. It did not find the logic error in the edge case, the security assumption at the API boundary, or the test that couldn't fail.

AI reviewing its own output is not code review. It's proofreading. The model shares the same blind spots as the code it wrote — same training, same patterns, same gaps.

Human review is not a legacy practice waiting to be automated. It's the check that catches what the AI can't see in itself.

## Keeping the Skill Sharp

The grumpy architect posture only works if it's maintained. A few things we found helped:

**Don't reduce review time because AI wrote it.** If anything, AI-generated code warrants more scrutiny, not less — the surface polish makes it easier to miss what's underneath.

**Review out loud occasionally.** Narrating what you're reading forces a level of engagement that silent reading doesn't. If you can't explain what a block of code does while you're reading it, that's a signal to slow down.

**When something fails in production, trace it back through review.** Was this reviewable? What would have caught it? That retrospective keeps the review practice honest.

**Rotate reviewers on a team.** If the same person always reviews AI output, the rest of the team's critical reading muscle goes unpractised. The skill needs to stay distributed.

**Hold the requester accountable for the output.** The person who asked the AI to write something is responsible for what it produced — not the AI. That framing keeps the human in the loop in a meaningful way, not just formally.

## What We Took Away

1. **Two passes: understand first, evaluate second** — you can't catch the gap between intent and implementation if you skip to judgment
2. **Push hardest on edges, unhappy paths, and boundaries** — the happy path is where AI is strongest; everything else is where errors hide
3. **Check what the tests actually test** — AI tests can pass by construction without testing meaningful behaviour
4. **AI reviewing AI is proofreading, not review** — shared blind spots mean shared misses
5. **The skill needs active maintenance** — time, rotation, retrospectives; it atrophies under reduced load just like any other skill

## What's Next

With the practice established, the next lesson looks at how to structure the feedback from review — communicating findings in a way that improves the next iteration rather than just cataloguing problems.
