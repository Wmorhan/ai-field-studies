# What AI Knows (and Doesn't)

Before you write a single prompt, it's worth understanding what your AI assistant actually knows — and where its knowledge stops cold.

## The training cutoff

Every AI model is trained on data up to a specific date. Before that date: broad knowledge of languages, frameworks, APIs, patterns. After it: nothing.

Not "less accurate." Not "somewhat outdated." Nothing.

The model doesn't know what it doesn't know. If a major library released a breaking change six months after its training cutoff, the AI will teach you the old API — correctly, confidently, and completely wrong for your version. It won't warn you. It won't hedge. It will just be wrong.

This is the first thing to internalize: **the AI's confidence is not a reliability signal.**
