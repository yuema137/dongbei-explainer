# Terminology and jargon policy

Default audience: technically literate science and engineering people who may not know this subfield.

## Decision rule

Ask two separate questions:

1. Is the term already familiar to this audience?
2. Does the reader understand the part of its mechanism needed here?

Knowing `GPU` does not imply knowing why VRAM can be full at 20% utilization. Explain the bottleneck, not GPU.

## Familiarity tiers

- Tier 1 — shared vocabulary: use directly. Provisional defaults include `LLM`, `agent`, `code`, `repo`, `bug`, `Git`, `GPU`, `CPU`, `model`, and `dataset`. Context can move a term between tiers.
- Tier 2 — broad but not universal: give one short, natural first-use explanation when it matters. Provisional examples: `worktree`, `rebase`, `CI`, `event loop`, `gradient accumulation`, `quantization`, `KV cache`, `regularization`.
- Specialist — domain-specific: explain only the amount needed for the current argument, possibly with formal detail. Examples include `Poisson regression offset`, memory ordering, or measure-theoretic terms.

These assignments are provisional until human calibration. The candidate deck in [`annotation/`](../../../annotation/README.md) lets readers label a large pool; it is a decision aid, not an authoritative dictionary.

## First meaningful use

Do not annotate a token merely because it appears in a filename. Explain it when the reasoning depends on it. Keep the exact English term and then reuse it normally.

Within the current conversation, do not redefine a term already explained well. If context may have been compacted, use a tiny reminder: “还是前面那个 `offset`——exposure 那一项。” Never create repository state just to remember terminology.

Do not repeatedly write `term（definition）`. Do not invent Chinese replacements for code identifiers, CLI commands, APIs, protocols, equations, or standard English jargon.
