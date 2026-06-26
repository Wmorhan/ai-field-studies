# Code Review in the Age of AI: Don't Get Comfortable

## What We Kept Seeing

There's a lot of conversation about AI taking programmers' jobs. We think that's the wrong thing to worry about. The more immediate risk isn't that AI replaces you — it's that you slowly, comfortably, let it replace the parts of your thinking that matter most.

It happens gradually. The AI produces something that looks right. You read it, it feels reasonable, you approve it. Next time, you spend a little less time looking. Then a little less again. The output keeps coming, fluent and confident, and the critical reading muscle quietly atrophies from disuse.

Nobody fired you. You just stopped doing the hard part.

## The Astrology Problem

Here's what we learned, and it took longer than it should have: plausible is not the same as correct.

AI output is optimised to sound right. It uses the correct terminology, the right structure, the appropriate level of detail. It reads like something written by someone who knows what they're doing. And that surface fluency triggers a cognitive shortcut we've all developed over years of working with humans: *if it sounds confident and coherent, it probably is.*

That shortcut works reasonably well with people. It doesn't work with AI.

The analogy that stuck with us was astrology. A horoscope is written to be recognisable. The language is general enough that you can map it onto your own situation, and because you're doing the mapping yourself, it feels accurate. You nod along. You think: yes, that does sound like me. But the text wasn't written about you. It was written to sound like it could be about anyone.

AI output does the same thing, technically. It produces the next most plausible sequence of tokens — the thing that fits the pattern of what correct output looks like. The model doesn't know when it's wrong. It has no mechanism for uncertainty that shows up in the text. A hallucination reads exactly like a correct answer. The confidence is identical because the generation process is identical.

We also noticed something subtler: sometimes you want it to be true. You asked for a solution. The AI gave you something that looks like a solution. There's a pull toward accepting it — because if it's right, you're done. That pull is worth naming, because it works against you every time.

## What Google and MIT Found

We're not the only ones who noticed this pattern.

MIT researchers studying AI-assisted knowledge work found that when people use AI for cognitively demanding tasks, they engage less deeply with the problem itself. The effect isn't laziness — it's how cognition works. When something plausible appears immediately, the brain reduces its own effort. The hard thinking that would have happened doesn't happen, because it no longer feels necessary.

Google, looking at internal patterns of AI-assisted development, raised concerns about skill deterioration among engineers who relied heavily on AI for code generation. The worry isn't a single bad decision — it's the gradual erosion of the ability to evaluate what the AI produces, precisely because that evaluation requires the same skills that are going unpractised.

The feedback loop closes on itself: the less you exercise critical evaluation, the less capable you become at it, the more you rely on the AI, the less you evaluate. This is the comfortable chair. It's not a dramatic collapse — it's a slow slide, and it feels fine the whole way down.

## The Team Dimension

For an individual, skill atrophy is a personal risk. For a team, it's a systemic one.

Code review exists in part because no one catches their own errors with the same reliability as a fresh set of eyes. The assumption built into the practice is that reviewers can actually read code critically — that they bring genuine scrutiny, not a formality.

If a team stops maintaining that capacity — because the AI produces good-looking output, because review starts feeling like rubber-stamping, because the critical reading muscle goes unpractised across the whole group — then the human check disappears from the system. What remains looks like code review. It has the same steps, the same approvals, the same merge gates. But it isn't doing what code review is supposed to do.

AI errors tend to be subtle and consistent. The model has systematic blind spots — things it gets wrong in similar ways across similar situations. A team that has maintained genuine critical evaluation catches these. A team that has learned to approve plausible output doesn't.

That gap, compounded over time, is a serious risk. Not a gradual degradation — a brittleness that holds until something fails badly enough to reveal it.

## The Posture That Prevents It

What we've found is that the antidote is an attitude, not a process.

The old grumpy architect attitude. The one that has been burned enough times by things that looked right but weren't, that it no longer uses "looks right" as a filter. The one that walks into a review not asking *does this look good?* but *where is it wrong?*

That's a fundamentally different starting posture, and the difference matters more than any checklist.

Looking for confirmation finds confirmation. Looking for failure finds failures. When you go into a review assuming there are errors — not hoping there aren't, not suspecting there might be, but assuming there are — you read differently. You push on things. You ask why. You follow the logic to its edges to see if it holds.

This posture predates AI. It's what good code review always required. What AI changes is the temptation to abandon it, because the output is more fluent, more complete, and more immediately satisfying than what a junior developer would have produced. The quality of the surface makes it easier to stop looking beneath it.

Don't stop looking beneath it.

## What We Took Away

1. **Plausible is not correct** — AI output is optimised to sound right; that's not the same as being right
2. **The comfortable slide is real** — skill atrophy happens gradually, feels fine, and is hard to notice from the inside
3. **Wanting it to be true is a bias** — the pull toward accepting a solution because you want to be done works against good review
4. **Team atrophy is systemic risk** — one person's critical thinking going unpractised is a gap; a whole team's is a missing check
5. **The posture is the practice** — assume there are errors and go looking for them; everything else follows from that

## What's Next

With the right posture established, the next lesson gets into what effective code review actually looks like with AI in the loop — where to focus, what to look for, and how to structure the habit so it doesn't erode. [Practical Code Review →](./02-practical-review.md)
