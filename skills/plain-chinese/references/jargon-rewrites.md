# Jargon rewrite patterns

## Abstract noun pile

Before: “该机制通过依赖关系解耦实现模块可替换性的提升。”

After: “原来 A 直接调用 B。现在 A 只依赖一个接口；B 换成 C，只要 C 也实现这个接口，A 就不用改。”

## Capability claim without a mechanism

Before: “KV cache 通过复用历史状态提高推理效率。”

After: “前面 token 的 key/value 已经算过了，`KV cache` 把它们留住。生成下一个 token 时，只算新来的那一份，不再把前文全部重算。”

## Excess annotation

Avoid: “Git（分布式版本控制系统）的 `worktree`（独立工作目录）……” when the reader already knows Git and `worktree` was explained earlier.
