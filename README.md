# dongbei-explainer

> **东北话不是目的。讲明白才是目的。**

`dongbei-explainer` 是一组可组合的 Agent Skills，用自然、具体、带一点东北口语节奏的中文解释技术问题。

我们在实际使用 AI 的过程中反复观察到：当你要求它“用东北大白话讲”，回答往往会少绕一点，少堆几层抽象名词，更愿意直接说清楚“谁干了啥、原来咋干、现在改了哪一步”。

这不是经过验证的语言学定律，也不是说东北话能提高模型推理能力。它是一个值得测试的实践假设。这个项目把其中真正有用的沟通习惯拆出来，做成可以复用、组合和校准的 skills：

- 别一上来扔定义，先说这东西到底干啥；
- 别堆名词，把参与者和动作说出来；
- 先讲原来怎么走，再讲现在改了哪一步；
- 给一个具体例子，让数据、控制或状态真走一遍；
- 正式术语该留就留，但第一次需要时马上讲明白；
- 说清它解决了啥，也说清它没解决啥。

目标读者是有一般 STEM 背景的人：能跟技术推理，但不一定学过计算机，也不需要熟悉正在解释的项目。

## 这不是什么

这不是东北方言表演包，也不是把每句话塞进“老铁、嘎嘎、咱就是说”。项目明确排除喜剧腔、强行模仿口音、晦涩地方词、装熟和居高临下。

输出应该首先是准确、好懂的技术解释。东北口语只负责把节奏拉得更直接、更像一个靠谱的人坐旁边跟你捋明白。

## 最快开始

### 在 Codex 或其他 coding agent 里

克隆仓库后，在项目根目录运行：

```bash
# Codex：安装到当前项目
scripts/install codex

# Claude Code：安装到当前项目
scripts/install claude-code
```

个人级安装，加 `--scope user`：

```bash
scripts/install codex --scope user
scripts/install claude-code --scope user
```

然后直接说：

```text
用 dongbei-explainer 给我解释这个 issue。假设我有一般 STEM 背景，
但不熟悉这个项目。先讲问题怎么发生，再讲这个改动改了哪一步。
```

也可以只用其中一层：

```text
用 clear-tech-explainer 解释这段代码，不要加东北风格。

用 plain-chinese 把这段文档改得不绕，但保留公式和英文术语。

给刚才的解释加 concrete-example，拿一条真实数据走一遍。

保持原来的技术内容，只加轻一点的 dongbei-voice。
```

安装脚本只是把同一份 canonical skill 链接或复制到宿主的发现目录，不会维护 Codex 版和 Claude Code 版两套 prompt。项目遵循 [Agent Skills 开放规范](https://agentskills.io/specification)。Claude Code 当前的项目级发现目录是 `.claude/skills/`；路径与扩展能力见[官方文档](https://code.claude.com/docs/en/slash-commands#where-skills-live)。

### 在支持 Skills 的网页聊天里

如果网页产品支持上传或安装 Agent Skills，把 `skills/` 下需要的目录作为 skill bundle 添加进去，然后直接说：

```text
使用 dongbei-explainer 解释下面的问题，Level 2，面向一般 STEM 读者。
```

完整模式需要这五个目录：

```text
skills/clear-tech-explainer
skills/plain-chinese
skills/concrete-example
skills/dongbei-voice
skills/dongbei-explainer
```

如果网页聊天不支持 Skills，也不用折腾安装：把相关 `SKILL.md` 和它链接的 reference 文件作为附件上传，再提出问题即可。最小组合是 `clear-tech-explainer + plain-chinese`；需要完整风格时再加 `concrete-example + dongbei-voice`。

OpenAI 当前也把可重复工作流作为 Skills 使用场景；参见 [OpenAI Docs / ChatGPT use cases](https://learn.chatgpt.com/use-cases)。不同网页产品的上传入口会变化，所以这里不绑定某个按钮名称。

### 不安装，临时用一次

最简单的请求方式：

```text
用清楚、自然、带一点东北口语节奏的中文解释下面的问题。
目标读者有一般 STEM 背景，但不一定懂计算机，也不了解这个项目。
先说原来发生了什么，再说真正卡在哪儿、现在改了哪一步；
拿一个具体对象走完整个过程。保留必要的英文术语、代码和公式，
项目内部黑话第一次出现时先用中文说明它负责什么。
不要喜剧化，不要堆东北词，也别把读者当笨蛋。
```

这能临时使用，但完整 skill 的术语记忆、深度控制、反例和校准约束更稳定。

## Demo 1：`asyncio.sleep(0)` 为啥没有立刻响应取消？

公开问题：[CPython issue #84977](https://github.com/python/cpython/issues/84977)。issue 中的现象是：task 已经被 `cancel()`，但一次 `await asyncio.sleep(0)` 之后没有马上抛出 `CancelledError`，往往还要再经过几轮 event loop。

普通技术回答可能是：

> `asyncio.sleep(0)` 使用优化过的调度路径，将 coroutine 重新调度到 event loop。取消请求及其相关 callback 可能需要多个 loop iteration 才能传播，因此 `CancelledError` 不保证在一次 `sleep(0)` 后立即出现。

`dongbei-explainer` 更希望这样讲：

> 先别把 `cancel()` 理解成“当场掐断”。它干的事更像是在 event loop 的待办队列里挂个牌子：这个 task 该取消了。
>
> `await asyncio.sleep(0)` 呢？它只保证当前 task 先把位置让出来，让 event loop 转一圈。问题在这儿：这一圈里可能还有恢复 task、处理 callback、再把取消异常送进去这几步，不是一个动作全干完。
>
> 你可以把 event loop 想成一个人按队列办事。你刚说“这单撤了”，不等于他手里正在处理的单子瞬间消失；撤单通知也得排进流程。CPython 这个 issue 里，维护者说明 `sleep(0)` 只让出一个 cycle，而相关恢复链可能要两三轮，所以多等几次才看到 `CancelledError`，属于预期调度行为。
>
> 真正该记住的是：`cancel()` 是请求取消，不是同步强杀；`sleep(0)` 是让出一次执行机会，也不是“把所有待处理 callback 清空”。如果你在 coroutine 里跑 CPU-heavy code，往里面塞 `sleep(0)` 也不是根治，应该把重活放到 thread 或 process executor。

这里的“一个人按队列办事”只负责建立顺序感，随后马上对应回 task、callback 和 event-loop cycle，没有拿比喻替代机制。Python 文档也明确提醒：CPU-bound blocking code 会拖住所有并发 task，应放到 executor 中处理。[官方 asyncio 开发文档](https://docs.python.org/3/library/asyncio-dev.html#running-blocking-code)

## Demo 2：监控只有 300 MiB，Kubernetes 为啥在 500 MiB 把 container OOMKilled？

公开问题：[kubernetes/kubernetes issue #114142](https://github.com/kubernetes/kubernetes/issues/114142)。报告里 dashboard 和 Prometheus 大约显示 300 MiB，但 pod 的 cgroup 记录接近 500 MiB，随后发生 OOM kill。

普通技术回答可能是：

> 该问题由监控指标和 cgroup memory accounting 的口径差异导致。Prometheus 展示的 container memory 指标可能未包含 page cache 或 pod cgroup 中的其他内存，而 kernel 根据 cgroup 总使用量执行 memory limit。

`dongbei-explainer` 更希望这样讲：

> 这事看着矛盾，其实是两块表量的不是一个东西。
>
> dashboard 上那条 300 MiB，可能主要是在看某个 container 的 working set；kernel 决定要不要 OOM kill 时，看的却是 cgroup 这本总账。issue 里直接读 cgroup，`memory.usage_in_bytes` 已经到了大约 501 MB，limit 是 500 MiB 左右。再往下拆，光匿名内存大约 322 MB，文件页又有约 182 MB，合起来就快顶线了。
>
> 打个短比方：dashboard 像只报“屋里家具占了多少”，cgroup limit 管的是“家具、纸箱和屋里其他东西加一块儿占多少”。你盯着家具只有 300，以为地方还多；房东按总占用一量，已经满了。
>
> 所以真正要对的是口径：图上展示的到底是 working set、RSS，还是 container/pod cgroup 的总使用量；memory limit 又落在哪一级 cgroup。OOM 没在跟 dashboard 抬杠，它按 kernel 自己记的那本账执行。这个解释也不能偷懒成“Prometheus 不准”——指标可能完全准确，只是它回答的不是同一个问题。

这个 demo 保留了 issue 里的真实数字，也说明了比喻的边界：决定 OOM 的仍是具体 cgroup 层级和 kernel accounting，不是“房间”本身。

## 五个可组合 Skills

| Skill | 负责什么 |
|---|---|
| `clear-tech-explainer` | 先把因果链、before/after、边界和 trade-off 搭对 |
| `plain-chinese` | 去掉名词堆和循环定义，按读者熟悉度处理术语 |
| `concrete-example` | 让一个 commit、request、tensor、数字或状态真走一遍 |
| `dongbei-voice` | 加入克制但能感知的东北口语节奏 |
| `dongbei-explainer` | 按顺序组合上面四层 |

语义和口吻刻意分开。你可以只要清楚，不要东北风格；也可以把 `dongbei-voice` 接到别的解释工作流上。详细架构见 [docs/architecture.md](docs/architecture.md)。

## 术语怎么处理

这不是 jargon 翻译系统。

- 标准英文术语保留英文；
- Tier 1 直接使用，不做 AI 教师式重复定义；
- Tier 2 在第一次真正需要时用一句话说明，后面直接复用；
- 项目自己发明的英文长标签不自动算标准术语，先用中文说它负责什么；
- 同一轮对话里已经解释过的词，不再从头讲一遍。

第一轮人工标注覆盖 223 个英文术语和 164 条中文表达。正式结果见 [technical jargon tiers](skills/plain-chinese/references/common-technical-jargon.md) 和 [expression boundary](skills/dongbei-voice/references/expression-boundaries.md)。这些是可继续修订的产品默认值，不是全民词典。

## 我们怎么校准

项目不是“写完 prompt，自己觉得不错，就算完成”。当前流程分两阶段：

1. **词汇边界**：标注哪些表达普通话用户能直接理解，哪些英文术语需要首次简释。
2. **完整解释对照**：针对真实技术材料生成 baseline 和 full skill 两版，盲评 A/B，记录信息丢失、术语负担、口语自然度和具体修改意见。

校准已经让设计发生过实际变化：

- `KV cache` 样例暴露了风格改写会漏掉剩余计算和显存代价，于是增加 information-preservation check；
- merge/rebase 的火车类比遮住了 commit identity，于是改回 commit graph；
- 第一轮真实 PR 对照把受众错设成 senior engineer，导致 `sidecar` 等项目黑话没人解释；现在默认受众已改为一般 STEM、可能无 CS 背景；
- 同一轮还证明了“加两句说白了”不等于东北大白话，voice 现在必须重新组织解释，而不是做表面替词。

评测材料和 rubric 在 [eval/](eval/README.md)，阶段二标注页在 [eval/phase2/](eval/phase2/README.md)。

## 研究边界

初步语言资料支持一个保守结论：真正有用的更可能是动作化、状态描写、短问答和明确语势，而不是堆地方词。研究记录见 [research/dongbei-language-notes.md](research/dongbei-language-notes.md)。

我们不声称“东北话已经被证明能提高 LLM reasoning”。更准确的说法是：

> 实践中，这种表达方式看起来会把模型推向更直接、更具体的解释；这个项目把观察变成可复用、可拆分、可测试的 explanation protocol。

## 验证与贡献

```bash
scripts/validate
scripts/validate_phase2 eval/phase2/bundles/<bundle>.json
scripts/lint_text path/to/answer.md
```

欢迎贡献普通话用户觉得自然或出戏的表达、面向一般 STEM 读者的真实案例、因简化而丢失的技术条件、更准确的类比，以及不同 agent runtime 的行为对照。

贡献方式见 [CONTRIBUTING.md](CONTRIBUTING.md)。项目采用 [MIT License](LICENSE)。
