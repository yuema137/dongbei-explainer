<p align="center">
  <img src="assets/dongbei-explainer-title.png" alt="dongbei-explainer：要把大象装冰箱拢共分几步" width="100%">
</p>

# dongbei-explainer

> **东北话不是目的。讲明白才是目的。**

`dongbei-explainer` 是一组可组合的 Agent Skills，用自然、具体、带一点东北口语节奏的中文解释技术问题。这里有两个同样重要的词：**东北话**负责把语气拉得直接、有人味；**大白话**负责让普通 STEM 读者不用先学一套书面黑话，就能跟上事情到底怎么发生。

我们在实际使用 AI 的过程中反复观察到：当你要求它“用东北大白话讲”，回答往往会少绕一点，少堆几层抽象名词，更愿意直接说清楚“谁干了啥、原来咋干、现在改了哪一步”。

这不是经过验证的语言学定律，也不是说东北话能提高模型推理能力。它是一个值得测试的实践假设。这个项目把其中真正有用的沟通习惯拆出来，做成可以复用、组合和校准的 skills：

- 别一上来扔定义，先说这东西到底干啥；
- 别堆名词，把参与者和动作说出来；
- 先讲原来怎么走，再讲现在改了哪一步；
- 给一个具体例子，让数据、控制或状态真走一遍；
- 正式术语该留就留，但第一次需要时马上讲明白；
- 术语外面的中文得像真人会说的话，不能自己再造“同步强杀”这种压缩黑话；
- 不用中文破折号往一句话中间硬塞补充说明，拆成真人会说的短句；
- 说清它解决了啥，也说清它没解决啥。

目标读者是有一般 STEM 背景的人：能跟技术推理，但不一定学过计算机，也不需要熟悉正在解释的项目。

## 这不是什么

这不是东北方言表演包，也不是把每句话塞进“老铁、嘎嘎、咱就是说”。项目明确排除喜剧腔、强行模仿口音、晦涩地方词、装熟和居高临下。

输出应该首先是准确、好懂的技术解释。东北口语只负责把节奏拉得更直接、更像一个靠谱的人坐旁边跟你捋明白。

## 最快开始

### 已经开着一个 Codex 或 Claude Code 会话

假设：

- `dongbei-explainer` 在 `/path/to/dongbei-explainer`；
- 你正在处理的项目在 `/path/to/your-project`；
- Codex 或 Claude Code 会话也是从 `/path/to/your-project` 打开的。

另开一个终端，把 skills 装进**你正在处理的项目**：

```bash
# 当前会话是 Codex
/path/to/dongbei-explainer/scripts/install codex --project /path/to/your-project

# 当前会话是 Claude Code
/path/to/dongbei-explainer/scripts/install claude-code --project /path/to/your-project
```

默认用软链接安装，所以你更新 `dongbei-explainer` 后，不用重复复制文件。

安装以后，回到 Codex 或 Claude Code 的**聊天输入框**，直接发一句自然语言就行：

```text
用 dongbei-explainer 解释这个 issue。面向一般 STEM 读者，先讲问题怎么发生。
```

这句话不是 CLI 命令，不需要在终端里运行。平时也可以更随意地说“用东北大白话给我讲讲这个 PR”。只要请求和 skill 的 description 对得上，agent 就应该自动加载它。

如果自动识别没有生效，再在**聊天输入框**里显式指定。Codex 输入 `$dongbei-explainer 解释这个 issue`，Claude Code 输入 `/dongbei-explainer 解释这个 issue`。这两个前缀只是可选的强制调用方式，不是每次都要写。

Claude Code 会监看启动时已经存在的 skill 目录；如果 `.claude/skills/` 是刚才才第一次创建的，重启一次 Claude Code，再回到聊天输入框使用它。这是 Claude Code [官方文档说明的加载边界](https://code.claude.com/docs/en/slash-commands#where-skills-live)。

Codex 是否会在一个已经运行的会话中立刻刷新刚装进项目的 skill，目前没有可核实的官方保证。先在聊天输入框里正常使用；如果当前会话没有识别它，就在同一项目中新开一个 Codex 会话。这是最稳妥的做法。

如果你现在就要用、不想重启，也可以直接让当前 agent 读取 canonical skill：

```text
请读取并使用
/path/to/dongbei-explainer/skills/dongbei-explainer/SKILL.md，
以及它要求组合的四个 sibling skills，然后解释下面的问题：……
```

这相当于本次会话手动加载；不会把 skill 永久安装到宿主里。

### 给另一个项目安装

在 `dongbei-explainer` 仓库里运行，并明确指出要在哪个项目里使用：

```bash
# Codex：安装到目标项目
scripts/install codex --project /path/to/your-project

# Claude Code：安装到目标项目
scripts/install claude-code --project /path/to/your-project
```

不加 `--project` 时，脚本会装到 `dongbei-explainer` 自己的项目级发现目录，主要用于开发和验证这些 skills。

不想给每个项目装一遍，可以做一次个人级安装：

```bash
scripts/install codex --scope user
scripts/install claude-code --scope user
```

安装完成后，重新打开或新建 coding-agent 会话，然后直接说：

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

公开问题：[CPython issue #84977](https://github.com/python/cpython/issues/84977)。issue 中的现象是：一个正在由 event loop 管理的 async task 已经被 `cancel()`，但一次 `await asyncio.sleep(0)` 之后没有马上抛出 `CancelledError`，往往还要再经过几轮 event loop。

普通技术回答可能是：

> `asyncio.sleep(0)` 使用优化过的调度路径，将 coroutine 重新调度到 event loop。取消请求及其相关 callback 可能需要多个 loop iteration 才能传播，因此 `CancelledError` 不保证在一次 `sleep(0)` 后立即出现。

`dongbei-explainer` 更希望这样讲：

> 这事儿到底卡在哪儿？你先别把 `cancel()` 当成“啪一下，当场掐断”。这玩意儿没那么干。event loop 是轮流安排 async task 往下跑的调度器；你调用 `cancel()`，只是往它的待办队列里挂个牌子：这个 task 该取消了。
>
> 那 `await asyncio.sleep(0)` 又干了啥？它只保证当前 task 先把位置让出来，让 event loop 转一圈。可这一圈里还排着好几步呢：“让 task 接着跑”“执行排队的 callback（回调函数）”“把取消异常送进 task”。这些活儿不是一把全整完，得按队列一个一个来。
>
> 打个比方，event loop 就像一个人搁窗口按号办事。你刚喊一句“我这单撤了”，他手里的单子不会原地消失；“办撤单”本身也得排到号。CPython 这个 issue 里就是这么回事：`sleep(0)` 只让 event loop 往前走一轮，前后几个 callback 可能摊在两三轮里。多等几轮才看到 `CancelledError`，不是取消没好使，是还没轮到那一步。
>
> 所以说白了，`cancel()` 省不掉“调度器处理取消”这一步；它只是告诉系统“这个 task 该停了”。`sleep(0)` 也只是先把位置让出去，不是让 event loop 把整条队列一次清空。coroutine 就是这种能暂停、以后再接着跑的函数。要是里面塞着一大段特别吃 CPU 的计算，那你隔几行硬插一个 `sleep(0)` 也治不了根。该交给 thread 或 process executor 的活儿，还得交出去。

这里的“一个人按队列办事”只负责把先后顺序讲明白，后面马上对应回 task、callback 和 event-loop cycle，没有拿比喻顶替机制。Python 文档也明确提醒：特别吃 CPU、又一直不交回控制权的代码，会让其他 async task 全跟着等；这类计算应该放到 executor 里。[官方 asyncio 开发文档](https://docs.python.org/3/library/asyncio-dev.html#running-blocking-code)

## Demo 2：监控只有 300 MiB，Kubernetes 为啥在 500 MiB 把 container OOMKilled？

公开问题：[kubernetes/kubernetes issue #114142](https://github.com/kubernetes/kubernetes/issues/114142)。报告里 dashboard 和 Prometheus 大约显示 300 MiB，但 pod 的 cgroup 记录接近 500 MiB，随后 kernel 因为内存超限执行了 OOM kill，把进程停掉。

普通技术回答可能是：

> 该问题由监控指标和 cgroup memory accounting 的口径差异导致。Prometheus 展示的 container memory 指标可能未包含 page cache 或 pod cgroup 中的其他内存，而 kernel 根据 cgroup 总使用量执行 memory limit。

`dongbei-explainer` 更希望这样讲：

> 这事儿瞅着挺怪：图上明明才 300 MiB，咋到 500 MiB 就给 container 干掉了？先别急着说监控不准。说白了，是两块表量的压根儿不是一个东西。
>
> dashboard 上那条 300 MiB，可能主要盯着 container 最近真正在用、又不容易回收的那部分内存，常见指标名叫 working set。可 kernel 判断要不要 OOM kill，翻的是 cgroup 记的总账。`cgroup` 是啥？你先把它理解成 Linux 给一组进程统一记资源账、顺手卡上限的东西。搁这个 issue 里一查，`memory.usage_in_bytes` 已经到大约 501 MB，limit 才 500 MiB 左右。再把账拆开看：程序自己放数据花了约 322 MB，读写文件留下的缓存页又占约 182 MB。这俩往一块儿一凑，可不就快顶线了吗？
>
> 你就把它想成一间屋：dashboard 只跟你报“家具占了多少”，cgroup limit 管的却是“家具、纸箱，再加屋里别的东西，总共占多少”。你一瞅家具才占 300，寻思地方还宽敞呢；可人家按全屋一量，已经塞满了。比喻只到这儿，真正触发 OOM 的还是 cgroup 记下来的总内存。
>
> 所以碰上这种事咋查？先看图上画的到底是啥：working set、RSS，还是整个 container/pod cgroup 的总内存。RSS 指进程眼下占着的物理内存。接着再看 500 MiB 的 limit 到底卡在哪一级。俩数可能谁都没算错：一个问“眼下有多少内存不容易收回来”，另一个问“这个 cgroup 总共记了多少”。kernel 按后面那本账办事，账到线了，它就 OOM kill。

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
