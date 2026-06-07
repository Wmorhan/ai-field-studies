# Design: Workflow Methodology — Structure, B-MAD, and Linear

**Date:** 2026-06-07  
**Output file:** `lessons/05-advanced/workflow-methodology.md`  
**Role:** Advanced lesson — assumes reader has completed the getting-started lessons and has basic AI-assisted coding experience.

---

## Purpose

Readers who've gotten past the basics hit a ceiling: AI produces working output that doesn't fit their process, their conventions, or their architecture. The root cause is under-specification. This lesson names that failure mode, reframes the reader's mental model (AI doesn't fatigue on detail), then introduces B-MAD and Linear as the practical system for working at the right level of structure.

---

## Structure

### Section 1 — The failure mode
A short, recognizable scenario: vague task → AI guesses → output is functional but foreign. Doesn't match the codebase style, doesn't follow the team process, requires more cleanup than if you'd done it yourself. No moralizing — just the problem stated plainly. Reader either recognizes it or fears it.

### Section 2 — The insight
Counter-intuitive reframe: AI doesn't get tired of detail. The constraint that limits documentation quality in human teams — people get bored, meetings run long, specs feel like overhead — simply doesn't exist with AI. You can never over-specify. Structure isn't overhead; it's input quality, which is the only lever you control. The more precisely you define work, the better AI performs. Every vague word in a task description is a guess AI has to make on your behalf.

### Section 3 — B-MAD: the methodology
What it is: "Build More Architect Dreams" — an AI-driven agile framework built around structured workflows and specialized agent roles (PM, Architect, Developer, UX, and more). The core philosophy: AI as expert collaborator who guides your thinking, not a tool that replaces it. Traditional AI tools do the thinking for you — average results. B-MAD provides the structure that brings out your best thinking in partnership with AI.

Brief lifecycle overview: brainstorming → product brief → architecture → implementation → deployment. Each phase has defined outputs that become the next phase's inputs. No deep dive — that's a future lesson. Goal here is to give the reader enough to understand why this structure matters, not how to execute every phase.

Why it fits AI-assisted work: it forces the structured thinking that makes AI outputs good. The deliverables at each phase (briefs, specs, architecture docs) are exactly the context AI needs to perform well.

Brief acknowledgment that other structured AI methodologies exist (e.g. other agile-AI frameworks, custom team processes). B-MAD is the author's preferred choice — the principle of structured, phase-based work applies regardless of which framework you use.

### Section 4 — Linear: the task layer
Linear as the single source of truth for what's being built. Epics map to B-MAD phases; tasks become the concrete inputs to AI sessions. When work lives in a structured tool with proper epics, acceptance criteria, and scope boundaries, you can hand AI exactly what it needs — not a verbal description, but a real specification.

The connection: B-MAD defines how you think through the work, Linear holds what you're building. Together they close the gap between "I have an idea" and "AI has the context it needs."

Brief acknowledgment that other project management tools serve the same purpose (Jira, GitHub Issues, Notion, etc.). What matters is that the work is structured and documented — not which tool holds it.

### Section 5 — What's Next / Further Reading
- Forward pointer to future B-MAD deep-dive lesson
- Links: B-MAD docs (https://docs.bmad-method.org/), B-MAD GitHub (https://github.com/bmad-code-org/bmad-method), Linear (https://linear.app)

---

## Tone and style

Match existing lesson style: direct, opinionated, no hedging. The failure mode scenario should be short and sharp — two to three sentences max. The insight section carries the philosophical weight; keep it punchy. B-MAD and Linear sections are practical, not promotional.

---

## Scope

Covers: failure mode, structure insight, B-MAD introduction, Linear as task layer. Does NOT cover: full B-MAD phase walkthrough (future lesson), Linear setup/configuration tutorial, comparison of Linear vs other tools.
