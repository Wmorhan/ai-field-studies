# Workflow Methodology Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Write `lessons/05-advanced/workflow-methodology.md` — an advanced lesson covering the structure-as-input-quality insight, B-MAD as the methodology, and Linear as the task layer.

**Architecture:** Single markdown file with five sections: failure mode → insight → B-MAD → Linear → closing. Problem-first narrative arc. Each section references the spec at `docs/superpowers/specs/2026-06-07-workflow-methodology-design.md`.

**Tech Stack:** Markdown. Tone reference: `lessons/05-advanced/configuration-strategies.md` and `lessons/01-getting-started/configure-claude-md.md`.

---

### Task 1: File scaffold and failure mode section

**Files:**
- Create: `lessons/05-advanced/workflow-methodology.md`
- Reference: `lessons/05-advanced/configuration-strategies.md` (tone and prerequisite callout style)

- [ ] **Step 1: Create the file with the opening section**

Write the following to `lessons/05-advanced/workflow-methodology.md`:

```markdown
# Workflow Methodology: Structure, B-MAD, and Linear

> **Prerequisite:** This lesson assumes you've completed [Configuring AI Agents: Setting Behavior Before You Code](../01-getting-started/configure-claude-md.md).

You hand the AI a task. It produces working output. But when you look at it, something is off — the structure doesn't match your architecture, the naming doesn't follow your conventions, the approach ignores a constraint you thought was obvious.

You spend the next hour cleaning it up. It would have been faster to do it yourself.

The problem isn't the AI. It's what you gave it to work with.
```

- [ ] **Step 2: Verify tone**

Read the opening of `lessons/05-advanced/configuration-strategies.md`. Check: short paragraphs, direct statements, problem named before solution, no hedging. The failure mode scenario should be three sentences max — sharp, not melodramatic.

- [ ] **Step 3: Commit**

```bash
git add lessons/05-advanced/workflow-methodology.md
git commit -m "Add workflow-methodology lesson: scaffold and failure mode"
```

---

### Task 2: The insight section

**Files:**
- Modify: `lessons/05-advanced/workflow-methodology.md`

- [ ] **Step 1: Append the insight section**

Append to `lessons/05-advanced/workflow-methodology.md`:

```markdown

## You can never over-specify

Here's what's different about AI: it doesn't get tired of detail.

With human collaborators, there's a real cost to over-documentation. Specs that are too long don't get read. Too many requirements in a ticket and the developer stops paying attention. Too much explanation and you're the person in the meeting who won't stop talking.

None of that applies to AI. Every word of context you provide is consumed equally. A three-sentence task description and a three-page specification are processed with the same attention. There is no fatigue, no impatience, no "I get it, just let me start."

This means the only constraint on specification quality is you. Every vague word in a task description is a decision you're handing to the AI. Every missing constraint is a guess it has to make on your behalf. The more precisely you define what you want, the less the AI has to invent.

Structure isn't overhead. It's input quality — the only lever you actually control.
```

- [ ] **Step 2: Verify the section flows from the failure mode**

Re-read from the top. The failure mode names the problem. This section should feel like the natural diagnosis — "here's why that happens and the counter-intuitive fix." If the transition feels abrupt, add one bridging sentence at the start of this section.

- [ ] **Step 3: Commit**

```bash
git add lessons/05-advanced/workflow-methodology.md
git commit -m "Add workflow-methodology lesson: insight section"
```

---

### Task 3: B-MAD section

**Files:**
- Modify: `lessons/05-advanced/workflow-methodology.md`

- [ ] **Step 1: Append the B-MAD section**

Append to `lessons/05-advanced/workflow-methodology.md`:

```markdown

## B-MAD: a methodology built for this

B-MAD ("Build More Architect Dreams") is an AI-driven agile framework built around structured workflows and specialized agent roles — PM, Architect, Developer, UX, and more.

The core philosophy cuts against how most people first use AI: instead of asking AI to do the thinking for you, B-MAD positions AI as an expert collaborator who guides your thinking. You bring the intent and the domain knowledge. AI brings structure, consistency, and execution. The outputs at each phase — briefs, specs, architecture documents — are exactly the context the next phase needs.

The lifecycle moves from brainstorming through product brief, architecture, implementation, and deployment. Each phase has defined deliverables. Each deliverable becomes structured input for the next. Nothing is left to interpretation.

A future lesson covers the phases in depth. For now, the key point: B-MAD works because it forces the structured thinking that makes AI outputs good. The methodology and the insight from the previous section are the same thing — write it down properly, and the AI can actually help.

Other structured AI methodologies exist, and the space is evolving fast. The principle holds regardless of which framework you use: phase-based work with defined deliverables is what separates purposeful AI output from generic AI output.
```

- [ ] **Step 2: Verify the B-MAD description is accurate and not promotional**

Check: does it explain what B-MAD is without overselling it? The "other methodologies exist" line should feel honest, not defensive. The forward pointer to a future lesson should be clear but brief.

- [ ] **Step 3: Commit**

```bash
git add lessons/05-advanced/workflow-methodology.md
git commit -m "Add workflow-methodology lesson: B-MAD section"
```

---

### Task 4: Linear section and closing

**Files:**
- Modify: `lessons/05-advanced/workflow-methodology.md`

- [ ] **Step 1: Append the Linear section and closing**

Append to `lessons/05-advanced/workflow-methodology.md`:

```markdown

## Linear: where the work lives

Methodology defines how you think through work. Linear is where that work lives.

Linear is a project management tool built around epics and tasks. In a B-MAD workflow, epics map to phases — a product brief epic, an architecture epic, an implementation epic. Tasks within each epic are the concrete units of work that become inputs to AI sessions.

This matters because of the insight above: the more structured your task, the better the AI performs. A task in Linear with a clear title, description, acceptance criteria, and scope boundary is a specification. When you hand that to AI, you're handing it the context it needs — not a verbal description reconstructed from memory.

The combination: B-MAD defines the structure of your thinking, Linear holds the artifacts. Together they close the gap between "I have an idea" and "AI has everything it needs to help."

Linear isn't the only tool that works here. Jira, GitHub Issues, Notion, or a well-structured markdown file can serve the same purpose. What matters is that work is documented with enough structure that you could hand it to someone with no prior context and they'd know exactly what to do. If it meets that bar, it meets the bar for AI.

## What's Next

A future lesson in this series goes deeper on B-MAD's phases — how to move from brief to architecture to implementation with AI at each step.

## Further Reading

- [B-MAD Method documentation](https://docs.bmad-method.org/) — full reference for the framework
- [B-MAD on GitHub](https://github.com/bmad-code-org/bmad-method) — open source, free to use
- [Linear](https://linear.app) — project management built for modern development teams
```

- [ ] **Step 2: Read the full lesson top to bottom**

Check: does the arc hold? Failure mode → insight → methodology → tool layer → closing. Does the "no prior context" test for tasks feel like a natural echo of the "you can never over-specify" insight? Adjust any transition that feels abrupt.

- [ ] **Step 3: Commit**

```bash
git add lessons/05-advanced/workflow-methodology.md
git commit -m "Add workflow-methodology lesson: Linear section and closing"
```
