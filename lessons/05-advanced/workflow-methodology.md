# Workflow Methodology: Structure, B-MAD, and Linear

> **Prerequisite:** This lesson assumes you've completed [Configuring AI Agents: Setting Behavior Before You Code](../01-getting-started/configure-claude-md.md).

You hand the AI a task. It produces working output. But when you look at it, something is off — the structure doesn't match your architecture, the naming doesn't follow your conventions, the approach ignores a constraint you thought was obvious.

You spend the next hour cleaning it up. It would have been faster to do it yourself.

The problem isn't the AI. It's what you gave it to work with.

## You can never over-specify

Here's what's different about AI: it doesn't get tired of detail.

With human collaborators, there's a real cost to over-documentation. Specs that are too long don't get read. Too many requirements in a ticket and the developer stops paying attention. Too much explanation and you're the person in the meeting who won't stop talking.

None of that applies to AI. Every word of context you provide is consumed equally. A three-sentence task description and a three-page specification are processed with the same attention. There is no fatigue, no impatience, no "I get it, just let me start."

This means the only constraint on specification quality is you. Every vague word in a task description is a decision you're handing to the AI. Every missing constraint is a guess it has to make on your behalf. The more precisely you define what you want, the less the AI has to invent.

Structure isn't overhead. It's input quality — the only lever you actually control.
