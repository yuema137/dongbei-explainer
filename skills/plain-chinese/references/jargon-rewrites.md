# Jargon rewrite patterns

## Abstract noun pile

Before: “该机制通过依赖关系解耦实现模块可替换性的提升。”

After: “原来 A 直接调用 B。现在 A 只依赖一个接口；B 换成 C，只要 C 也实现这个接口，A 就不用改。”

## Capability claim without a mechanism

Before: “KV cache 通过复用历史状态提高推理效率。”

After: “前面 token 的 key/value 已经算过了，`KV cache` 把它们留住。生成下一个 token 时，只算新来的那一份，不再把前文全部重算。”

## Excess annotation

Avoid: “Git（分布式版本控制系统）的 `worktree`（独立工作目录）……” when the reader already knows Git and `worktree` was explained earlier.

## Compressed pseudo-plain Chinese

Avoid: “`cancel()` 不是同步强杀。”

Prefer: “调用 `cancel()` 只是提出取消请求，不是这行代码一跑，task 就当场停掉。”

Avoid: “将配置语义外置并完成执行态持久化。”

Prefer: “这条配置原来写死在代码里；现在可以从外面传进来，而且 run 过程中会把实际用到的值写下来。”

The English terms are not the problem. The problem is surrounding them with newly invented Chinese shorthand that creates another layer to decode.
