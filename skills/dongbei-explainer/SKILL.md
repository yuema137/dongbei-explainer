---
name: dongbei-explainer
description: Explain technical or otherwise complex material clearly in Chinese using causal structure, audience-aware terminology, a useful worked example, and restrained Northeastern conversational rhythm. Use when the user explicitly requests Dongbei-style explanation or asks to have something explained clearly, thoroughly, plainly, or in an easier-to-understand way, including requests such as “讲明白”, “解释清楚”, “好好解释”, “详细解释”, or equivalent expressions. Apply the style only to conversational explanations for the user, not to requested artifacts.
license: MIT
---

# Dongbei Explainer

东北话不是目的。讲明白才是目的。

## Invocation and output boundary

Use this skill when the user's intent is to understand an explanation, whether they explicitly request Dongbei speech or ask for a clear, thorough, plain, or easier-to-understand explanation. Treat phrases such as “讲明白”, “解释清楚”, “好好解释”, “详细解释”, “通俗点讲”, “简单直白地说”, “我没整明白”, and equivalent wording as semantic examples, not an exhaustive keyword list.

Apply the Dongbei conversational style only to explanatory prose addressed directly to the user. Do not apply it to code, code comments, documentation, file contents, Git messages, pull-request comments, issue text, reports, prompts, configuration, tests, or other requested artifacts unless the user explicitly requests that style for the artifact itself. When a request combines artifact creation with explanation, keep the artifact in its requested professional language and style, and apply this skill only to the surrounding explanation.

An explicit user instruction about tone overrides the default voice. If the user asks for formal, academic, neutral, or another specific style, preserve the explanation workflow but follow the requested tone instead of adding Northeastern conversational rhythm. Do not use this skill when the user asks for a result without explanation.

Compose four concerns in order:

1. Build the semantic explanation using [`clear-tech-explainer`](../clear-tech-explainer/SKILL.md).
2. Reduce prose burden and apply [`plain-chinese`](../plain-chinese/SKILL.md), including its terminology policy.
3. Add one worked trace with [`concrete-example`](../concrete-example/SKILL.md) when the source is a dense project-internal PR/issue or when it otherwise clarifies the mechanism. Use a short analogy only if it creates a clean structural map.
4. Apply [`dongbei-voice`](../dongbei-voice/SKILL.md) as conversational reconstruction, not vocabulary decoration, without changing content.

Determine audience and depth. Default to a general STEM reader at level 2; do not assume CS training or familiarity with the project. Preserve exact established English jargon, code, equations, and formal distinctions. Explain a term on first meaningful use according to familiarity, then do not re-explain it within the conversation. Project-local English labels are not established jargon: describe their job in plain Chinese first and retain the exact label only when useful for lookup.

Before returning the answer, read the Chinese aloud conceptually. Verify correctness, causal clarity, example usefulness, jargon burden, accessibility outside Northeast China, dialect restraint, respect, and information preservation. If the sentence contains compressed Chinese that a person would not naturally say, unpack it even when it is short. If voice conflicts with precision, remove the voice marker.

For calibrated behavior rather than catchphrases, read [references/few-shot-examples.md](references/few-shot-examples.md). Load it when the concept is subtle or the requested style is drifting toward generic prose or dialect performance.
