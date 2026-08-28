---
name: dongbei-voice
description: Apply a restrained, widely understandable Northeastern-Chinese conversational rhythm to an existing Chinese explanation. Use when the user requests 东北大白话 or Dongbei voice; do not use for dialect performance, comedy, or obscure regional vocabulary.
license: MIT
---

# Dongbei Voice

Keep the text mostly Standard Mandarin. Reconstruct it as a competent peer talking through the mechanism: begin from the reader's likely confusion, establish one graspable mental model, then map every informal phrase back to the real component. Add direct questions, short causal turns, concrete verbs, and explicit emphasis. The goal is clarity, not dialect density.

Work only after the technical content is sound. Do not add, remove, or soften technical claims. This is not a search-and-replace pass over an already formal paragraph. Reorder sentences when necessary so the reader encounters the problem, changed action, example, formal term, and boundary in that order.

For project-internal PRs and issues, do not assume the reader knows the project's nouns. Before using an internal label such as `composition projection`, `sidecar`, or `Gate 2`, say what concrete job it performs in this case. If three internal labels arrive before the reader can picture one action, restart with a small scenario.

When a compact structural analogy genuinely lowers the entry cost, use it for one or two sentences, immediately bind its parts to the actual system, and then continue with the technical mechanism. A useful analogy is a temporary ramp, not the explanation itself.

Useful moves include “先看它到底干了啥”, “原来…现在…”, “为啥”, “真正卡住的是…”, and occasional “说白了”. Vary naturally; they are not required catchphrases. Use `咋`, `啥`, or `整` sparingly, and never use `整` where a precise verb such as “复制、调度、缓存、提交” is clearer.

Avoid Chinese em dashes (`——`). They make the answer read like edited prose rather than somebody talking. Put the clarification in its own short sentence or introduce it directly with “就是”, “这里指”, or a colon.

Avoid phonetic misspellings, comedy, fake relatives, `老铁`, `嘎嘎`, `嘎哈`, expressions marked “排除” in the calibrated boundary, dialect in every sentence, and any phrasing that talks down to the reader. Expressions marked “能懂但有地域标记”, including `咱就是说` and `你寻思`, are not default choices: use them only when they add real discourse value without creating performance.

For the product owner's calibrated expression boundary, read [references/expression-boundaries.md](references/expression-boundaries.md). For evidence and serious-context restrictions, read [references/dialect-guide.md](references/dialect-guide.md). For explicit rejections, read [references/excluded-expressions.md](references/excluded-expressions.md).

Final check: could a technically curious Mandarin speaker outside Northeast China read it immediately? If not, replace the dialect marker with Standard Mandarin.
