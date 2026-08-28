---
name: clear-tech-explainer
description: Explain technical concepts in Chinese through concrete causal structure, before/after mechanisms, boundaries, and trade-offs. Use for explanation, teaching, onboarding, or rewriting dense technical prose; do not add regional voice unless requested.
license: MIT
---

# Clear Tech Explainer

Make the reader understand what changes and why. Technical correctness outranks ease or tone.

Before writing, determine the audience and requested depth. If neither is stated, assume a reader with general STEM background who can follow technical reasoning but may have no computer-science training and no familiarity with this project. Default to level 2.

## Depth

- Level 1: what it is, why it matters, and one boundary.
- Level 2: mechanism step by step, with a small trace when useful.
- Level 3: actual control/data flow, structures, code, or equations.
- Level 4: intuitive entry plus complete formal distinctions and limitations.

Build only the relevant parts of this reasoning spine; do not print it as eight mandatory headings:

1. What job does it do?
2. What happened before it existed or was used?
3. Where did the old approach fail?
4. Which step did it add, remove, or change?
5. How does one concrete item move through it?
6. What is the easiest misconception?
7. What does it solve, and what remains unsolved?
8. What does it cost?

Prefer actors, verbs, causal chains, explicit before/after comparisons, and one main idea per sentence. Introduce a formal term when it becomes useful, explain it according to the audience, then reuse it exactly. Preserve code, equations, APIs, and standard English terminology.

STEM literacy does not imply software-engineering vocabulary or project familiarity. The default reader may not know `watchdog`, `sidecar`, `runtime`, `composition projection`, or `Gate 2`. Explain the concrete actor and responsibility on first meaningful use; do not treat internal labels as shared jargon.

End with a preservation check: compare the explanation to the source concept and restore any condition, distinction, or trade-off lost during simplification.

For recurring structures and failure modes, read [references/explanation-patterns.md](references/explanation-patterns.md) and [references/anti-patterns.md](references/anti-patterns.md).
