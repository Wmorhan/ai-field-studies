# Supply Chain Attacks: Compromising the Foundation

> **Previous:** [Shared Configurations](./04-shared-configurations.md)

## Why This Matters

The previous lessons cover attacks that target your session, your configuration, your tools. Supply chain attacks don't bother with any of that. They compromise the components you depend on — packages, models, infrastructure — before you ever interact with them. One compromised component reaches every user downstream, simultaneously, invisibly.

This is the threat that scales.

## What the Supply Chain Actually Is

Most developers think of the supply chain as "the model." It's much wider:

- The AI client itself (Claude Code is an npm package with its own dependency tree)
- MCP servers you've installed
- Every package those MCP servers depend on, and their dependencies
- Orchestration frameworks connecting components (Langchain, LlamaIndex, and similar)
- The runtime environments — Node.js, Python, the OS
- Model serving infrastructure for self-hosted or local models
- Data sources feeding RAG pipelines or tool outputs
- Editor extensions that sit alongside AI tooling

Any node in that graph is an attack surface. A compromise anywhere propagates to every user downstream.

## Attack Patterns That Apply Directly to AI Tooling

**Typosquatting** — attackers register `anthropics`, `claude-codes`, `langchian` on npm or PyPI. A developer miskeys a package name during setup. The malicious package installs silently. It's in the dependency tree of every project that ran that install. This is already happening to AI-related packages.

**Dependency confusion** — organizations use private internal packages. Attackers publish packages with the same names to public registries. Build systems that check public registries first pull the malicious version. An MCP server your team built internally may have internal dependencies. Those names are targets.

**Maintainer account compromise** — a popular MCP server has a legitimate, trustworthy maintainer. Their npm account gets compromised via credential stuffing or phishing. A new version is published with a malicious payload. Every user with auto-updates enabled gets it. The package's history looks clean — only the latest version is poisoned.

**The XZ Utils pattern** — the most sophisticated variant. An attacker spends months or years building genuine trust in an open source project: fixing real bugs, improving documentation, becoming a recognized contributor. Then inserts a backdoor. The 2024 XZ Utils attack did exactly this, targeting SSH infrastructure. The pattern is patient, hard to detect, and fully applicable to AI tooling maintainers.

## The Model Weight Problem

This is where AI supply chain diverges fundamentally from traditional software security. Code can be reviewed, compiled deterministically, scanned with static analysis. Model weights cannot.

Model weights are billions of floating-point numbers encoding behavior in ways we don't fully understand. A backdoored model can:

- Behave completely normally under all standard test conditions
- Activate malicious behavior only when a specific trigger phrase or input pattern appears
- Pass every benchmark, every safety evaluation, every red team test — until the trigger fires

Researchers have demonstrated this works. It's called a "sleeper agent" or "Trojan model." A model fine-tuned on poisoned data, or with subtly modified weights, carries dormant behavior that no external audit will catch.

For Claude specifically, Anthropic controls the training pipeline — that's a meaningful protection. But the threat is directly relevant for:

- Open-source models (Llama, Mistral, Qwen) downloaded from Hugging Face
- Community fine-tunes on those base models
- Local model serving via Ollama, vLLM, LM Studio
- Any third-party model you run or integrate with

Hugging Face has already found uploaded models containing executable code that ran on load — the file format was supposed to prevent this. The attack surface is real and active.

## How Supply Chain Completes the Chain

The previous lessons required effort from the attacker: plant content in a webpage, poison a knowledge base, get a malicious config into a community repo, compromise an MCP server.

Supply chain attacks remove most of that effort. A compromised MCP package returns whatever the attacker wants into Claude's context, automatically, for every user, every session, without any further action. The attacker ships once; the attack runs indefinitely.

Combined with the tool attack surface from the previous lesson: a compromised tool package doesn't need to inject into Claude's context to manipulate behavior. It can act directly, with whatever system access the tool has been granted, and return legitimate-looking results to Claude.

The threat stack compounds:
- Injection (chapter 2) requires planting content somewhere Claude reads it
- Tools (chapter 3) give that injection execution capability
- Shared configs (chapter 4) give it persistent reach across sessions
- Supply chain (this chapter) makes it systemic — one compromise, every user

## Staying on Top of What Your Tools Depend On

The user's framing from the start of this series is the right one: you need to understand what tools Claude is using and what those tools depend on. This is active maintenance, not a one-time setup.

**Know what you're running.** Every MCP server, every package in its dependency tree. This is the software bill of materials (SBOM) concept applied to AI agent tooling. It's not paranoid — it's basic hygiene for anything running with significant system access.

**Pin versions.** Use `package-lock.json`, `poetry.lock`, pinned Docker image digests. Don't let AI tooling update silently. Review what changed before it runs. A dependency update is a trust decision.

**Audit regularly.** `npm audit`, `pip-audit`, Dependabot alerts. These catch known-compromised packages in your dependency tree. They don't catch zero-days, but they catch the cases where the community already knows something is wrong.

**Minimize the footprint.** Every MCP server you don't install is an attack surface that doesn't exist. Every dependency you don't pull in is a package that can't be compromised in your environment. Ruthlessly minimize what your AI agent depends on and has access to.

**Verify provenance.** Who maintains this MCP server? What's their release history? Is there a security policy? When was it last updated? An abandoned package with 50 transitive dependencies is a liability, not a tool.

**Watch for anomalies.** Unexpected network calls from a tool. File access outside the expected scope. Responses that look instruction-shaped rather than data-shaped. These are signals worth investigating.

**For models specifically: trust the source.** Use models from providers with verifiable training pipelines. For open-source models, prefer those from established organizations with documented training processes over anonymous community fine-tunes. Treat a model from an unknown Hugging Face account the same way you'd treat a binary from an unknown domain.

## Key Takeaways

1. **The supply chain is wider than the model** — client packages, MCP servers, dependencies, runtimes, and data sources are all in scope
2. **Compromising one component reaches every downstream user** — this is the threat that scales
3. **Model weights are opaque** — backdoored weights can pass every test until a trigger fires; there is no code review equivalent
4. **Supply chain completes the injection chain** — a compromised tool package doesn't need to inject; it acts directly
5. **Active maintenance is required** — pinned versions, dependency audits, provenance checks, anomaly monitoring; this is ongoing work, not a one-time setup

## What's Next

This series has covered the five major threat layers for AI-assisted development. Each builds on the previous — and the most serious real-world attacks combine multiple layers simultaneously. The practical posture: understand the full stack from model weights to configuration files, apply least privilege at every level, and treat AI tooling with the same scrutiny you'd apply to any software running with significant system access.

## Further Reading

- SLSA (Supply-chain Levels for Software Artifacts) — a framework for reasoning about and improving supply chain security; directly applicable to AI tooling dependency chains
- SBOM (Software Bill of Materials) standards — SPDX and CycloneDX specifications for tracking dependencies
- "Sleeper agents: training deceptive LLMs that persist through safety training" — Anthropic research paper on backdoored model behavior
- OWASP LLM Top 10, LLM03: Training Data Poisoning — covers the model-level supply chain threat
- Hugging Face security blog — documentation of real malicious model uploads and detection approaches
