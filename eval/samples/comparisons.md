# Variant comparisons

These curated artifacts test what each layer should add. They are not claimed as raw outputs from a particular model.

## KV cache

**A — default:** `KV cache` stores intermediate representations to optimize autoregressive inference through computational reuse.

**B — plain core:** 生成下一个 token 时，前面 token 的 key/value 已经算过。`KV cache` 把它们留下，避免从头重算。它换来的是显存占用随 context 增长。

**C — plain + concrete:** 生成第 101 个 token：缓存里已有前 100 个 token 各层的 key/value；模型只为第 101 个算新的一份，再对 101 份做 attention。省掉的是前 100 份 key/value 的重复计算，不是让 attention 完全不随 context 增长。

**D — plain + Dongbei:** 先看它到底留了啥：前面 token 算过的 key/value。下一个 token 来了，老的别重算，只补新的一份。真正省的是重复计算；context 越长，缓存占的显存照样涨。

**E — full:** 和 C 的技术 trace 一致，再采用 D 的短问答节奏；不能丢掉“各层”、attention 仍读取全部历史位置、显存增长这些信息。

Observation: B fixes most jargon burden. C exposes the exact saved computation. D improves pacing but is not independently more complete. Initial D omitted the residual attention work; calibration added the explicit “没变成常数开销” preservation rule.

## Git merge vs rebase

**A — default:** Merge preserves topology whereas rebase linearizes history by replaying commits.

**B — plain core:** `merge` 把两条历史接起来，通常新增一个 merge commit。`rebase` 则把 D、E 的改动依次应用到新 base 上，生成 D'、E'；内容可能相同，但 parent 和 hash 变了。

**C — plain + concrete:**

```text
A--B--C          A--B--C------M       A--B--C--D'--E'
    \       ->       \       /   or
     D--E              D-----E
```

**D — plain + Dongbei:** 原来 D、E 从 B 岔出去。`merge` 是把两条线接上；`rebase` 不是把原 commit 搬家，是按新 parent 重做 D'、E'。所以 hash 变了。共享出去的历史别随便 rebase，别人手里的线对不上。

**E — full:** 使用 C 的图和 D 的解释，并明确 merge 在 fast-forward 等情况下未必生成 merge commit。

Observation: a train analogy hid object identity. The commit graph replaced it. Calibration also changed “merge adds a commit” to “when needed”.

## GPU memory vs utilization

**A — default:** Memory allocation and compute utilization measure orthogonal resource dimensions.

**B — plain core:** 显存占用是“现在有多少数据留在 GPU 上”；utilization 是“采样窗口里 GPU 有多少时间在执行 kernel”。参数和缓存可以占满显存，同时 GPU 等 CPU、数据或同步，所以 utilization 只有 20%。

**C — plain + concrete:** 一个 100 ms 窗口里，模型参数始终占 22 GB；GPU 只运行 kernel 20 ms，其余 80 ms 等 DataLoader。图上就可能同时看到 22 GB 和约 20% utilization。

**D — plain + Dongbei:** 显存满，只说明东西都搁那儿了，不说明 GPU 一直在干活。真正卡住的可能是 DataLoader：100 ms 里算了 20 ms，剩下 80 ms 在等，utilization 自然就低。

**E — full:** 使用 C 的时窗，并补充工具采样口径、异步执行和 kernel 间空洞。

Observation: Dongbei wording helps separate static capacity from activity, but `搁那儿` alone is less exact. The revised version immediately names resident parameters/cache and waiting stages.

## Poisson regression offset

**A — default:** The offset is a fixed-coefficient covariate accounting for heterogeneous exposure.

**B — plain core:** 观察 1000 小时和 10 小时的事件数不能直接比。用 `log E[Y_i] = log(exposure_i) + x_i^T beta`，`log(exposure_i)` 的系数固定为 1，所以模型拟合的是单位 exposure 的 rate。

**C — plain + concrete:** 城市 A 1000 小时发生 20 次，B 10 小时发生 2 次；裸事件数像是 A 更多，rate 却是 0.02/h 和 0.2/h。offset 把观察机会放进均值结构。

**D — plain + Dongbei:** 公式先别扔，先看两边观察时长一不一样。差 100 倍还硬比事件数，结论肯定跑偏。`offset` 就把 exposure 那一项明确放进模型，系数固定为 1。

**E — full:** 合并 B/C/D，并明确 offset 不估计 exposure 的系数，也不解决 overdispersion 或 confounding。

Observation: analogy would add no value; numbers plus equation are clearer. Expert mode must not postpone the equation for more than one setup sentence.
