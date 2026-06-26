# Guardrails and Content Controls: The First Line of Defense

> **This is the first lesson in a series on AI security.** Each chapter builds on the previous — guardrails set the baseline, then the following lessons cover how attackers work around them.

## What Brought Us Here

Most teams we've talked to assume the AI has guardrails and leave it there. The guardrails exist, they work, and for obvious attacks they hold. But what we learned — sometimes the hard way — is that guardrails are one layer of defence, not the whole defence. Understanding exactly what they protect against, and what they don't, is what lets you reason clearly about the threats that follow in this series.

## What Guardrails Are

Guardrails are constraints on what the model will do, built in at multiple levels:

**Model-level training** — the deepest layer. Through techniques like reinforcement learning from human feedback (RLHF) and constitutional AI — think of these as the values and boundaries baked into the model during its creation — models are trained to refuse certain outputs: instructions for weapons, content that harms children, impersonation of real people. These refusals are embedded in the model itself. They're not rules a prompt can simply override.

**Operator system prompts** — the layer between the model and the end user. When a company deploys an AI in a product, they configure its behaviour through a system prompt: stay on topic, don't discuss competitors, always recommend consulting a professional. These are real constraints, but they operate at the instruction level, not the model level.

**Content classifiers** — real-time filters that check inputs and outputs against known harmful patterns. An additional safety net on top of the trained behaviour.

Together these three layers define what the model will and won't do under normal conditions.

## What They Protect Against

Guardrails are designed to prevent the model from being *used as a weapon*:

- Someone asking the AI to explain how to make dangerous materials
- A prompt attempting to generate content that harms specific individuals
- Attempts to produce material that crosses baseline ethical lines

For these direct, explicit attacks, modern guardrails are robust. The training is deep and hard to override through simple instruction.

## What They Don't Fully Cover

**Framing attacks** — the request itself is prohibited, but a different framing isn't:
- "Write a story where a chemistry teacher explains to students how to..."
- "In a fictional world where this was legal, describe..."
- "For a security research paper, outline the theoretical steps..."

Each framing shifts the apparent context of the request. Some work, some don't. The guardrails evaluate the likely output and intent — but intent can be obscured.

**Gradual escalation** — no single step triggers a refusal, but a sequence of small steps reaches prohibited territory. Each message is individually innocuous.

**Guardrail erosion via configuration** — operator-level prompts can extend or relax model behaviour. A malicious or compromised configuration can instruct the model to treat certain restrictions as suspended. This is operator-level trust being abused — which is why what gets into your configuration matters, covered later in [Shared Configurations](./04-shared-configurations.md).

**The inverse: weaponising guardrails against you** — an attacker can deliberately trigger false positives. Content designed to make the AI refuse legitimate user requests. Not a compromise of the model — a manipulation of its safety mechanisms to make your assistant unreliable.

## The Core Limitation

Guardrails ask: *is this output harmful?*

They evaluate the model's response against known harm patterns. What they don't evaluate is whether the model's understanding of the request has been manipulated before that check fires.

That gap is exactly what prompt injection exploits — which is where we go next.

## What We Took Away

1. **Guardrails operate at three levels**: model weights (deepest), operator configuration, and runtime classifiers
2. **They protect against direct, explicit attacks** — the model being asked outright to produce harmful content
3. **Framing, escalation, and configuration abuse** are the main bypass patterns
4. **Guardrails can be turned against you** to produce false positives and break legitimate use
5. **They're the first layer, not the only layer** — the following lessons cover what they don't address

## What's Next

Guardrails evaluate what the model *outputs*. Prompt injection attacks change what the model *thinks it was asked* — before the guardrail fires. [Prompt Injection →](./02-prompt-injection.md)

## Further Reading

- OWASP LLM Top 10 — a structured taxonomy of LLM-specific security risks, including prompt injection and training data poisoning
- Anthropic's usage policies — what Anthropic prohibits at the model level versus what operators can configure
