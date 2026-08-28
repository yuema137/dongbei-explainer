# Initial calibration findings

This pass was a structured self-review of the curated variants, not a blinded model study.

## Revisions caused by examples

1. **Voice must run last.** An early KV-cache voice draft sounded direct but lost residual attention cost and per-layer memory. The preset now builds semantics first and performs an information-preservation check after styling.
2. **Exact verbs beat `整`.** In systems cases, `整一下` erased whether the operation was allocate, schedule, cache, or commit. `dongbei-voice` now explicitly forbids this substitution.
3. **Graphs beat forced analogies.** A merge/rebase train analogy obscured that rebased commits are new objects. The example layer now prefers a commit graph.
4. **Plain language supplies most of the gain.** Across all four comparisons, variant B removes the main comprehension barrier. Voice mainly adds pacing and salience. Skills remain separate for this reason.
5. **Expert depth needs early formal detail.** The first offset draft delayed the equation too long. Level 3–4 guidance now treats conversation as an entrance, not a replacement.
6. **Terminology and mechanism are separate.** GPU is Tier 1, yet its utilization mechanism still needs explanation. Multi-turn cases explicitly test that distinction.

## Product-owner boundary round

The complete `2026-08-28.1` card round replaced provisional vocabulary judgments with an explicit Mandarin-user boundary. In particular, `worktree`, `rebase`, and `KV cache` became Tier 1 while `event loop`, `dependency inversion`, and `gradient accumulation` became Tier 2. Several expressions initially hard-excluded by research caution moved to the “understandable but regionally marked” group. See [`research/human-calibration-notes.md`](../research/human-calibration-notes.md).

## Open questions

- Dialect naturalness needs ratings from speakers across Northeast China and from non-Northeastern Mandarin readers.
- Tier boundaries need evidence from real cross-domain conversations.
- Live Codex/Claude Code runs are still needed; identical source portability is testable locally, behavioral portability is not yet demonstrated.
- Density may need genre-sensitive rules rather than a single heuristic.
