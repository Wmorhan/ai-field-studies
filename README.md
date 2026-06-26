# AI Field Studies

Lessons learned and experiences from coding with AI tools, primarily focused on Claude Code.

## About

This repository documents practical insights, patterns, and real-world experiences from developing software with AI assistance. Content is aimed primarily at developers new to AI-assisted coding, with some advanced topics for experienced users.

## Lessons

> **New here?** Start with [Before everything starts](lessons/Before%20everything%20starts.md), then follow the order below.

### Getting Started
- [Before everything starts](lessons/Before%20everything%20starts.md) — Roles, speed, and validation in an AI-assisted world
- [What AI Knows (and Doesn't)](lessons/01-getting-started/what-ai-knows.md) — Training cutoffs, live data, and the conventions gap
- [Configuring AI Agents: Setting Behavior Before You Code](lessons/01-getting-started/configure-claude-md.md) — CLAUDE.md setup and why it matters

### Context
- [The Intent Layer](lessons/02-context/intent-layer.md) — Why and how documentation that keeps AI on track

### Code Review
- [Code Review in the Age of AI: Don't Get Comfortable](lessons/04-code-review/01-introduction.md) — Skill atrophy, the astrology problem, and why the grumpy architect attitude matters more than ever

### Security
- [Guardrails and Content Controls](lessons/03-security/01-guardrails.md) — The first line of defense: what guardrails protect against and what they don't
- [Prompt Injection](lessons/03-security/02-prompt-injection.md) — Direct vs indirect injection, real-world cases, why it's architecturally hard to fix
- [The Tool Attack Surface](lessons/03-security/03-tool-attack-surface.md) — How MCP tools transform injection from words into actions
- [Shared Configurations](lessons/03-security/04-shared-configurations.md) — Community configs, inherited trust chains, and your data leaving the session
- [Supply Chain Attacks](lessons/03-security/05-supply-chain.md) — Compromising the packages, models, and infrastructure AI agents depend on

### Advanced
- [Scaling Your Configuration](lessons/05-advanced/configuration-strategies.md) — CLAUDE.md vs AGENTS.md, monorepo hierarchy
- [Workflow Methodology: Structure, B-MAD, and Linear](lessons/05-advanced/workflow-methodology.md) — Structure as input quality, B-MAD framework, Linear as task layer

---

## Structure

### `/lessons/`
Core lessons organized by topic. Mix of narrative writeups and structured guides:
- **01-getting-started/** - First steps with AI coding tools
- **02-context/** - Documentation, context, and memory for AI agents
- **05-advanced/** - Advanced techniques and workflows
- **03-security/** - Threat landscape for AI-assisted development
- **04-code-review/** - Maintaining critical evaluation skills in an AI-assisted world

### `/case-studies/`
Real-world projects and problems solved with AI assistance. Each includes context, approach, results, and lessons learned.

### `/patterns/`
Proven patterns and common pitfalls — coming soon.

### `/tools/`
Coverage of AI coding tools, guides, and comparisons — coming soon.

### `/resources/`
Links, references, and further reading.

## Contributing

This is a personal collection of experiences, but suggestions and discussions are welcome via issues.

## License

[To be determined]
