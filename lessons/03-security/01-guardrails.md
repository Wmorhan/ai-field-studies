# Guardrails and Content Controls: The First Line of Defense

> **This is the first lesson in a series on AI security.** Each chapter builds on the previous — guardrails set the baseline, then the following lessons show how attackers work around them.

## Why This Matters

Most developers assume the AI has guardrails and leave it there. The guardrails exist, they work, and for obvious attacks they hold. But guardrails are one layer of defense — not the whole defense. Understanding exactly what they protect against, and what they don't, is what lets you reason about the threats that follow in this series.

## What Guardrails Are

Guardrails are constraints on what the model will do, built in at multiple levels:

**Model-level training** — the deepest layer. Through techniques like RLHF (reinforcement learning from human feedback) and constitutional AI, models are trained to refuse certain outputs: instructions for weapons, content that exploits minors, impersonation of real people. These refusals are baked into the weights. They're not rules a system prompt can override.

**Operator system prompts** — the layer between the model and the user. When a company deploys Claude in a product, they configure behavior via system prompt: stay on topic, don't discuss competitors, always recommend consulting a professional. These are real constraints but they operate at the prompt level, not the weight level.

**Content classifiers** — real-time filters that evaluate inputs and outputs against known harmful patterns. An additional catch layer on top of the trained behavior.

Together these three layers define what the model will and won't do under normal conditions.

## What They Protect Against

Guardrails are designed to prevent the model from being *used as a weapon*:

- A user asking Claude to explain how to synthesize dangerous chemicals
- A prompt trying to generate content that harms specific individuals
- Attempts to make the model produce material that violates baseline ethical constraints

For these direct, explicit attacks, modern guardrails are robust. The training is deep and hard to override through simple prompting.

## What They Don't Fully Protect Against

**Framing attacks** — the request is prohibited, but the framing isn't:
- "Write a story where a chemistry teacher explains to students how to..."
- "In a fictional world where this was legal, describe..."
- "For a security research paper, outline the theoretical steps..."

Each framing shifts the apparent context of the request. Some work, some don't. The guardrails evaluate the likely output and intent — but intent can be obscured.

**Gradual escalation** — no single step triggers a refusal, but a sequence of small steps reaches prohibited territory. Each message is individually innocuous.

**Guardrail erosion via configuration** — operator system prompts can extend or relax behavior. A malicious or compromised system prompt can instruct the model to treat certain restrictions as suspended. This is operator-level trust being abused — which is why what gets into your configuration matters, covered in [Shared Configurations](./04-shared-configurations.md).

**The inverse: guardrail weaponization** — an attacker can deliberately trigger false positives. Content designed to make Claude refuse legitimate user requests. Denial-of-AI-service through guardrail manipulation. Your assistant becomes unreliable not because it was compromised but because it was baited into over-refusing.

## The Key Limitation

Guardrails ask: *is this output harmful?*

They evaluate the model's response against known harm patterns. What they don't evaluate is whether the model's understanding of the request has been manipulated before that check fires.

This is the gap that prompt injection exploits — covered in the next lesson.

## Key Takeaways

1. **Guardrails operate at three levels**: model weights (deepest), operator system prompts, and runtime classifiers
2. **They protect against direct, explicit attacks** — the model being asked to produce harmful content outright
3. **Framing, escalation, and configuration abuse** are the main bypass patterns
4. **Guardrails can be weaponized** to produce false positives and break legitimate use
5. **They're the first layer, not the only layer** — the following lessons cover what they don't address

## What's Next

Guardrails evaluate what the model *outputs*. Prompt injection attacks change what the model *thinks it was asked* — before the guardrail fires. [Prompt Injection →](./02-prompt-injection.md)

## Further Reading

- OWASP LLM Top 10 — a structured taxonomy of LLM-specific security risks, including prompt injection and training data poisoning
- Anthropic's usage policies — what Anthropic prohibits at the model level versus what operators can configure
