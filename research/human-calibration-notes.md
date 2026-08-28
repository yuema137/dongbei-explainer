# Human boundary calibration: 2026-08-28.1

The product owner completed every card in the initial candidate set: 164 Dongbei/conversational expressions and 223 English technical terms. This project targets ordinary Mandarin users, not dialect authenticity, so this product-owner pass is the initial canonical boundary.

## Results

- Expressions: 115 directly usable, 18 understandable but regionally marked, 1 unclear/local, 30 excluded.
- Terms: 133 Tier 1 (use directly), 90 Tier 2 (brief first-meaningful-use explanation).
- `挂住了` was marked unclear/local with the note that its intended meaning was not fully understood. It must not appear in generated explanations.

## Changes from research priors

- `咋`, `啥`, `整`, and `搁这儿` moved from cautious candidates to directly understandable. They still remain subject to precision and density constraints.
- `咱就是说`, `你寻思`, `咋地`, and `老鼻子` are not hard exclusions; they are understandable but strongly marked. The skill now treats them as rare contextual options rather than defaults.
- `worktree`, `rebase`, `KV cache`, `p-value`, and `confidence interval` are Tier 1 for this audience. The explainer should not define them merely on first appearance, though a question about their mechanism must still explain that mechanism.
- `VRAM`, `event loop`, `dependency inversion`, `gradient accumulation`, `DDP`, `overdispersion`, and similar cross-specialty terms are Tier 2.
- No term required a third specialist tier in this candidate set. The decision rule retains an escape hatch for future terms outside the calibrated list.

The normalized export is stored in `eval/annotations/2026-08-28.1.json`. Generated reference files include the dataset version so later rounds can be compared rather than silently overwriting policy.
