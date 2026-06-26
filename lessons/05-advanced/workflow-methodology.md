# Workflow Methodology: Structure, B-MAD, and Linear

> **Prerequisite:** This lesson assumes you've read [Configuring AI Agents: Setting Behavior Before You Code](../01-getting-started/configure-claude-md.md).

We've all been there. You hand the AI a task. It produces working output. But something is off — the structure doesn't match your architecture, the naming doesn't follow your conventions, the approach ignores a constraint you thought was obvious.

You spend the next hour cleaning it up. It would have been faster to do it yourself.

The problem wasn't the AI. It was what we gave it to work with.

## You can never over-specify

Here's something that took us a while to fully internalise: the AI doesn't get tired of detail.

With human collaborators, over-documentation has a real cost. Specs that are too long don't get read. Too many requirements in a ticket and the developer stops paying attention. Too much explanation and you've become the person in the meeting who won't stop talking.

None of that applies to AI. Every word of context is consumed equally. A three-sentence task description and a three-page specification are processed with the same attention. There is no fatigue, no impatience, no "I get it, just let me start."

What this means in practice: the only constraint on how much context you provide is you. Every vague word in a task is a decision you're handing to the AI. Every missing constraint is a guess it has to make on your behalf. The more precisely something is defined, the less the AI has to invent.

Structure isn't overhead. It's input quality — and it's the main lever we actually control.

## B-MAD: a methodology built for this

B-MAD ("Build More Architect Dreams") is an AI-driven agile framework built around structured workflows and specialised agent roles — PM, Architect, Developer, UX, and more.

The core philosophy cuts against how most people first approach AI: instead of asking AI to do the thinking for you, B-MAD positions AI as an expert collaborator who guides your thinking. You bring the intent and the domain knowledge. AI brings structure, consistency, and execution. The outputs at each phase — briefs, specs, architecture documents — are exactly the context the next phase needs.

The lifecycle moves from brainstorming through product brief, architecture, implementation, and deployment. Each phase has defined deliverables. Each deliverable becomes structured input for the next. Nothing is left to interpretation.

A future lesson covers the phases in depth. For now, the key point: B-MAD works because it forces the structured thinking that makes AI outputs useful. The methodology and the insight from the previous section are the same thing — write it down properly, and the AI can actually help.

Other structured AI methodologies exist, and the space is evolving fast. The principle holds regardless of which framework you use: phase-based work with defined deliverables is what separates purposeful AI output from generic AI output.

## Linear: where the work lives

Methodology defines how you think through work. Linear is where that work lives.

Linear is a project management tool built around epics and tasks. In a B-MAD workflow, epics map to phases — a product brief epic, an architecture epic, an implementation epic. Tasks within each epic are the concrete units of work that become inputs to AI sessions.

This matters because of the earlier insight: the more structured the task, the better the AI performs. A task in Linear with a clear title, description, acceptance criteria, and scope boundary is a specification. When you hand that to AI, you're handing it the context it needs — not a verbal description reconstructed from memory.

The combination: B-MAD defines the structure of thinking, Linear holds the artifacts. Together they close the gap between "we have an idea" and "the AI has everything it needs to help."

Linear isn't the only tool that works here. Jira, GitHub Issues, Notion, or a well-structured markdown file can serve the same purpose. What matters is that work is documented with enough structure that you could hand it to someone with no prior context and they'd know exactly what to do. If it meets that bar, it meets the bar for AI.

## What's Next

A future lesson in this series goes deeper on B-MAD's phases — how to move from brief to architecture to implementation with AI at each step.

## Further Reading

- [B-MAD Method documentation](https://docs.bmad-method.org/) — full reference for the framework
- [B-MAD on GitHub](https://github.com/bmad-code-org/bmad-method) — open source, free to use
- [Linear](https://linear.app) — project management built for modern development teams
