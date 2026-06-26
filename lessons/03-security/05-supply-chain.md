# Supply Chain Attacks: Compromising the Foundation

> **Previous:** [Shared Configurations](./04-shared-configurations.md)

## The Threat That Scales

The previous lessons cover attacks that target your session, your configuration, your tools. Supply chain attacks don't bother with any of that. They compromise the components you depend on — packages, models, infrastructure — before you ever interact with them.

One compromised component reaches every user downstream, simultaneously, invisibly. This is the threat that scales.

## What the Supply Chain Actually Is

Most people think of the supply chain as "the model." We found it's much wider than that:

- The AI client itself (Claude Code, for instance, is a software package with its own dependency tree)
- Tool servers you've installed
- Every software package those tool servers depend on, and their dependencies
- Frameworks connecting AI components (Langchain, LlamaIndex, and similar)
- The runtime environments — Node.js, Python, the operating system
- Model serving infrastructure for self-hosted or local models
- Data sources feeding AI retrieval pipelines
- Editor extensions sitting alongside AI tooling

Any node in that graph is an attack surface. A compromise anywhere propagates to every user downstream.

## Attack Patterns We've Seen Applied to AI Tooling

**Typosquatting** — attackers register package names that look like legitimate AI packages: one letter off, a missing hyphen, a common misspelling. A developer miskeys a name during setup. The malicious package installs silently alongside legitimate tooling. It's in the dependency tree of every project that ran that install. This is already happening to AI-related packages.

**Dependency confusion** — organisations use privately named internal packages. Attackers publish packages with the same names to public repositories. Build systems that check public sources first pull the malicious version instead. A tool server your team built internally may rely on internal package names. Those names become targets.

**Maintainer account compromise** — a popular tool server or AI utility has a legitimate, trustworthy maintainer. Their account gets taken over through credential theft or phishing. A new version is published with a malicious payload. Every user with auto-updates enabled receives it. The package's history looks clean — only the latest version is poisoned.

**The long-game pattern** — the most sophisticated variant, and the hardest to defend against. An attacker spends months or years building genuine credibility in an open source project: fixing real bugs, improving documentation, earning trust. Then inserts a backdoor. The 2024 XZ Utils attack did exactly this, targeting SSH infrastructure used by millions of servers. The same patient approach will be applied to AI tooling.

## The Model Weight Problem

This is where AI supply chain diverges from traditional software security in a fundamental way. Code can be reviewed, compiled deterministically, scanned. Model weights — the actual "intelligence" of the AI — cannot.

Model weights are billions of numerical values encoding behaviour in ways we don't fully understand. A backdoored model can:

- Behave completely normally under all standard conditions
- Activate harmful behaviour only when a specific trigger phrase or pattern appears
- Pass every benchmark, every safety evaluation, every test — until the trigger fires

Researchers have demonstrated this works. It's sometimes called a "sleeper agent" model. A model trained on poisoned data, or one with subtly modified weights, carries dormant behaviour that no external review will catch.

For cloud-hosted models like Claude, the provider controls the training pipeline — that's meaningful protection. But this threat is directly relevant for:

- Open-source models downloaded from public repositories
- Community fine-tuned versions of those models
- Models run locally through tools like Ollama or similar
- Any third-party model integrated into your workflow

There have already been cases of models uploaded to public repositories containing code that executed when the model was loaded. The attack surface is real and active.

## How Supply Chain Completes the Chain

The earlier lessons each required some effort from the attacker: plant content in a webpage, poison a knowledge base, get a malicious config into a community repo.

Supply chain attacks remove most of that. A compromised tool package returns whatever the attacker wants into the AI's context, automatically, for every user, every session, with no further action required. The attacker ships once; the attack runs until someone notices.

Combined with tool access: a compromised tool package doesn't even need to inject instructions into the AI's context. It can act directly, with whatever system access it's been granted, and return legitimate-looking results. The AI never knew anything was wrong.

The threat stack compounds:
- Injection requires planting content somewhere the AI reads it
- Tools give that content execution capability
- Shared configs give it persistent reach across sessions
- Supply chain makes it systemic — one compromise, every user

## Staying on Top of What Your Tools Depend On

What we've found is that this requires active, ongoing attention — not a one-time setup check.

**Know what you're running.** Every tool server, every package it depends on. In traditional software, this is called a software bill of materials — a complete list of everything in your stack. The same concept applies to AI tooling. If you don't know what you're running, you can't know what's been compromised.

**Pin versions.** Use lock files and pinned package versions. Don't let AI tooling update automatically without review. A dependency update is a trust decision, not just a maintenance task.

**Audit regularly.** Tools exist to check whether packages in your dependency tree have known vulnerabilities or have been reported as compromised. Use them. They don't catch everything, but they catch what's already known.

**Minimise the footprint.** Every tool server you don't install is an attack surface that doesn't exist. Every dependency you don't pull in is a package that can't be compromised in your environment. The smaller the stack, the smaller the exposure.

**Verify where things come from.** Who maintains this tool server? What's their track record? When was it last updated? Is there a security contact? An abandoned package with dozens of dependencies is a risk, not a resource.

**Watch for things that don't fit.** Unexpected network calls from a tool. File access outside what the tool should need. Responses that seem to contain instructions rather than data. These are signals worth investigating rather than ignoring.

**For models specifically: trust the source.** Use models from providers with transparent training processes. For open-source models, prefer those from established organisations over anonymous community uploads. Treat a model from an unknown source the same way you'd treat an executable from an unknown website.

## What We Took Away

1. **The supply chain is wider than the model** — client packages, tool servers, dependencies, runtimes, and data sources are all in scope
2. **One compromised component reaches every user** — this is what makes supply chain attacks different in kind, not just degree
3. **Model weights are opaque** — backdoored models can pass every test until a trigger fires; there is no code review equivalent
4. **Supply chain completes the injection chain** — a compromised tool package doesn't need to inject; it acts directly
5. **Active maintenance is the only defence** — pinned versions, dependency audits, provenance checks, anomaly monitoring; this is ongoing work, not a checkbox

## Closing the Series

This series has walked through five layers of threat: guardrails, prompt injection, tool attack surfaces, shared configurations, and supply chain. The pattern across all of them is the same — the AI is powerful, its trust model is broad, and that combination creates opportunities for exploitation at every layer.

The practical posture isn't paralysis. It's informed use: understand the full stack, apply least privilege at every level, treat external inputs with scepticism, and maintain the same discipline around AI tooling that good security practice demands of any software with significant access to your environment.

## Further Reading

- SLSA (Supply-chain Levels for Software Artifacts) — a framework for reasoning about and improving supply chain security; applicable to AI tooling dependency chains
- "Sleeper agents: training deceptive LLMs that persist through safety training" — Anthropic research paper on backdoored model behaviour
- OWASP LLM Top 10, LLM03: Training Data Poisoning — covers the model-level supply chain threat
- Hugging Face security blog — documentation of real malicious model uploads and detection approaches
