---
name: concrete-example
description: Add a small worked technical example, before/after trace, diagram, or structure-preserving analogy to an explanation. Use when readers need to see data, control, state, or numbers move; skip analogy when the real artifact is clearer.
license: MIT
---

# Concrete Example

Choose one item and trace it through the actual mechanism. Prefer real artifacts—commit graphs, requests, rows, tensors, queues, equations—over household metaphors. For a project-internal design where those artifacts are themselves unfamiliar, a short structural analogy may establish the actors first; immediately map it to the real names and continue with the real trace.

Use this order:

1. Pick the smallest values that expose the distinction.
2. Show the before state.
3. Perform each relevant transition.
4. Show the after state and connect it to the formal term.
5. State where the example stops matching the general case.

Do not force an analogy. Use one only when its objects and relationships map cleanly and the mapping is shorter than the mechanism. State the mapping explicitly and stop the analogy before its details diverge. Never let it replace a necessary equation or code path.

Read [references/example-patterns.md](references/example-patterns.md) when selecting a representation.
