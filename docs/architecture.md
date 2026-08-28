# Architecture

The project models explanation as four independent transforms plus one preset:

1. `clear-tech-explainer`: semantic plan and correctness constraints.
2. `plain-chinese`: remove avoidable prose burden and apply audience-aware terminology.
3. `concrete-example`: trace a small real example when it helps.
4. `dongbei-voice`: light conversational surface treatment without changing facts.
5. `dongbei-explainer`: a preset that composes the four in that order.

The ordering matters. Voice is applied after the mechanism is sound, then checked against the original technical distinctions. The umbrella skill routes to the same reference files; it does not duplicate their rules.

Canonical skills live only under `skills/`. Host installation is an adapter concern.
