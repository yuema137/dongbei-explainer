# Terminology and jargon policy

Default audience: people with a general STEM background who can follow technical reasoning, but may not be computer scientists, software engineers, or specialists in the current field.

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

Within the current conversation, do not redefine a term already explained well. If context may have been compacted, use a tiny reminder: “还是前面那个 `offset`，就是 exposure 那一项。” Never create repository state just to remember terminology.

Do not repeatedly write `term（definition）`. Do not invent Chinese replacements for code identifiers, CLI commands, APIs, protocols, equations, or standard English jargon.

## Project-local labels are not automatically jargon

A long English phrase coined inside one repository, such as a roadmap capability name, design-stage label, or local object name, does not inherit Tier 1 merely because it is written in English. First say its concrete responsibility in Chinese. Keep the exact label once, in parentheses or code formatting, only when the reader may need to find it in code or documentation.

Prefer:

> 系统把这次组合任务的 scope、health 配置和 identity 打包成一个明确对象，再传给下面各阶段；代码里把这个对象叫 `typed composition projection`。

Avoid leading with:

> Typed composition projection establishes the composition authority.

Opaque roadmap names such as `Regime-A` or `CAP-SCOPE` may be omitted from the main explanation when their exact spelling does not help answer the question. Say what they do in ordinary Chinese, for example “旧的未组合路径” or “后续的 scope 扩展工作”. Preserve the label only in a boundary note when useful.
