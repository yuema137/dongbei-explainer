# Calibrated few-shot examples

## Dependency inversion

Dense/default:

> Dependency inversion introduces abstractions to decouple high-level policy from low-level implementation, improving extensibility and maintainability.

Better plain:

> 原来订单代码里直接写死“调用 Stripe”。换支付渠道时，订单代码也得改。`dependency inversion` 改的是依赖方向：订单代码只声明“我需要一个能收费的对象”；Stripe 和别的渠道各自实现这个接口。它降低了替换支付渠道时的联动修改，但接口设计和适配代码仍然要维护。

Full voice:

> 先看原来卡在哪儿：订单代码直接去找 Stripe，Stripe 一换，订单代码也跟着动。`dependency inversion` 干的事，是让订单代码别认具体厂商，只认“能收费”这个接口。Stripe、别的渠道谁满足接口谁接上。说白了，它拆掉的是这根写死的线，不是让依赖凭空没了；接口和适配器照样得有人维护。

## KV cache

Dense/default:

> KV cache stores historical key-value states to avoid redundant autoregressive attention computation.

Better plain:

> 生成第 101 个 token 时，前 100 个 token 的 key/value 已经算过。`KV cache` 把这些结果留在显存里，所以这一步只算新 token 的 key/value，再和缓存里的历史结果做 attention。它省的是重复计算；上下文越长，缓存本身仍会占更多显存。

Full voice:

> 这玩意儿到底缓存啥？不是把答案存起来，是把前面 token 已经算过的 key/value 留着。到第 101 个 token，只算新来的那一份，再拿它去看前 100 份。真正省掉的是“把老账重新算一遍”；老账越多，占的显存照样往上涨。

## Poisson regression offset (expert depth)

Dense/default:

> An offset accounts for heterogeneous exposure by including a fixed coefficient term in the linear predictor.

Better plain:

> 两个城市分别观察 1000 小时和 10 小时，事件数不能直接比。Poisson 模型可写成 `log E[Y_i] = log(exposure_i) + x_i^T beta`。这里 `log(exposure_i)` 是 `offset`：它的系数固定为 1，把模型目标从事件数改成单位 exposure 下的 rate。它校正观察机会不同，但不会自动处理 overdispersion 或遗漏变量。

Full voice:

> 公式先留着，咱先看 `offset` 到底补了哪一步。一个城市观察 1000 小时，另一个只观察 10 小时，事件数当然不能硬比。写成 `log E[Y_i] = log(exposure_i) + x_i^T beta`，`log(exposure_i)` 就是那个 `offset`，系数固定为 1。这样模型比的是 rate，不是假装两边观察时长一样。它没顺手解决 overdispersion，也没替你补上漏掉的变量。

## Negative calibration

Reject “老铁，这 KV cache 嘎嘎猛，缓存一下就完事了”：it neither says what is cached nor preserves memory cost. Reject a generic textbook definition followed only by dialect particles. The voice version must change discourse structure, not decorate sentences.
