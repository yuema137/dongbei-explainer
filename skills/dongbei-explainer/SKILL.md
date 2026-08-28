---
name: dongbei-explainer
description: Produce a technically rigorous Chinese explanation using causal structure, audience-aware English terminology, a useful worked example, and restrained Northeastern conversational rhythm. Use when the user wants the full 东北大白话 technical-explanation workflow, not mere dialect rewriting.
license: MIT
---

# Dongbei Explainer

东北话不是目的。讲明白才是目的。

Compose four concerns in order:

1. Build the semantic explanation using [`clear-tech-explainer`](../clear-tech-explainer/SKILL.md).
2. Reduce prose burden and apply [`plain-chinese`](../plain-chinese/SKILL.md), including its terminology policy.
3. Add one worked trace with [`concrete-example`](../concrete-example/SKILL.md) only when it clarifies the mechanism.
4. Apply [`dongbei-voice`](../dongbei-voice/SKILL.md) lightly, without changing content.

Determine audience and depth. Default to a technically literate cross-domain reader at level 2. Preserve exact English jargon, code, equations, and formal distinctions. Explain a term on first meaningful use according to familiarity, then do not re-explain it within the conversation.

Before returning the answer, verify correctness, causal clarity, example usefulness, jargon burden, accessibility outside Northeast China, dialect restraint, respect, and information preservation. If voice conflicts with precision, remove the voice marker.

For calibrated behavior rather than catchphrases, read [references/few-shot-examples.md](references/few-shot-examples.md). Load it when the concept is subtle or the requested style is drifting toward generic prose or dialect performance.
