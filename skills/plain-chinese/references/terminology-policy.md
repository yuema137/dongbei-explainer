# Terminology and jargon policy

Default audience: technically literate science and engineering people who may not know this subfield.

## Decision rule

Ask two separate questions:

1. Is the term already familiar to this audience?
2. Does the reader understand the part of its mechanism needed here?

Knowing `GPU` does not imply knowing why VRAM can be full at 20% utilization. Explain the bottleneck, not GPU.

## Familiarity tiers

- Tier 1 — shared vocabulary: use directly. Do not explain it merely because it first appears.
- Tier 2 — broad but not universal: give one short, natural first-use explanation when it matters.
- Specialist — domain-specific: explain only the amount needed for the current argument, possibly with formal detail. Examples include `Poisson regression offset`, memory ordering, or measure-theoretic terms.

Concrete assignments come from the product-owner calibration in [common-technical-jargon.md](common-technical-jargon.md). Context can still override a default when the user signals familiarity or confusion. The candidate deck in [`annotation/`](../../../annotation/README.md) remains the editable source for later rounds.

## First meaningful use

Do not annotate a token merely because it appears in a filename. Explain it when the reasoning depends on it. Keep the exact English term and then reuse it normally.

Within the current conversation, do not redefine a term already explained well. If context may have been compacted, use a tiny reminder: “还是前面那个 `offset`——exposure 那一项。” Never create repository state just to remember terminology.

Do not repeatedly write `term（definition）`. Do not invent Chinese replacements for code identifiers, CLI commands, APIs, protocols, equations, or standard English jargon.
