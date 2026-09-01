<p align="center">
  <img src="assets/dongbei-explainer-title.png" alt="dongbei-explainer：要把大象装冰箱拢共分几步" width="100%">
</p>

# DongbeiGPT

> **别管名字多唬人，先看它到底干了啥。**

AI 讲技术经常有个毛病：每个词单拿出来你都认识，连一块儿就不知道它到底说了啥。定义背了一串，事情是怎么发生的，一步也没给你捋。

我们平时用 AI 时发现，跟它说一句“用东北大白话讲”，回答往往一下就顺溜了。它不那么爱堆抽象名词了，开始老老实实告诉你谁干了啥，原来咋走，现在又改了哪一步。

这招既然好使，就不能每次全靠临时提醒。`dongbei-explainer` 把这套讲法拆成几份能组合的 Agent Skills。里面既有怎么把技术机制捋清楚，也有怎么说得像大白话，最后才是那一点东北口语节奏。

## 这个 skill 能干啥

主要就管这些事：

- 别一上来扔定义，先说这东西到底干啥；
- 别堆名词，把参与者和动作说出来；
- 先讲原来怎么走，再讲现在改了哪一步；
- 给一个具体例子，让数据、控制或状态真走一遍；
- 正式术语该留就留，但第一次需要时马上讲明白；
- 术语外面的中文得像真人会说的话，不能自己再造“同步强杀”这种压缩黑话；
- 不用中文破折号往一句话中间硬塞补充说明，拆成真人会说的短句；
- 说清它解决了啥，也说清它没解决啥。

默认读者有一般 STEM 背景，技术推理能跟上，但不一定学过计算机，更不该被要求先熟悉眼前这个项目。

## 这个 skill 不能干啥

不是每句话多塞几个“老铁、嘎嘎、咱就是说”，就叫东北大白话。那叫演，而且还耽误理解。晦涩地方词、硬学口音、假装跟读者很熟，这些都不要。

咱要的是一个懂技术的人坐你旁边，把事情从头到尾捋明白。该留的英文术语得留，该上的公式照样上。哪句话用了东北表达反而更费解，马上换回普通话。

还有一件事得说明白。目前没有证据证明“东北话能提高模型推理能力”。我们只有一个从实际使用里来的观察：这种说话方式经常能把模型往直接、具体的解释上拽。这个项目就是把它做成一套能复用、能测试、也能随时改的办法。

## 我们还真把赵本山小品拆开看了

光凭印象琢磨东北话，太容易写成网络段子。我们干脆找了五个大家熟悉的小品，看看里面的话咋就一听能明白：

- [《钟点工》](research/corpus/zhongdian-gong-notes.md)：先问清到底干啥，再拿一个小场景顺着往下走；
- [《昨天今天明天》](research/corpus/zuotian-jintian-mingtian-notes.md)：抽象说法没听懂，就换成过去、现在、以后各说什么；
- [《卖拐》](research/corpus/mai-guai-notes.md)：问句短一点，动作拆小一点，关键词重复时得往前推进；
- [《火炬手》](research/corpus/huo-ju-shou-notes.md)：一个信号对应一个动作，相近说法放在一起对照；
- [《说事儿》](research/corpus/shuo-shi-er-notes.md)：别光说“很大、很多、很厉害”，把数字和实际发生的事摆出来。

我们学的是这个说话节奏，不是收集包袱。小品里的口音写法、损人话、谐音梗和之前标成排除的词，一个都不能因为“原作里说过”就混进输出。完整台词也不放进仓库，只保留分析笔记。

## 已经有项目了，咋装

### Codex 或 Claude Code 会话已经开着了

先对一下路径：

- `dongbei-explainer` 在 `/path/to/dongbei-explainer`；
- 你正在处理的项目在 `/path/to/your-project`；
- Codex 或 Claude Code 会话也是从 `/path/to/your-project` 打开的。

另开一个终端，把 skills 装进**你正在处理的那个项目**：

```bash
# 当前会话是 Codex
/path/to/dongbei-explainer/scripts/install codex --project /path/to/your-project

# 当前会话是 Claude Code
/path/to/dongbei-explainer/scripts/install claude-code --project /path/to/your-project
```

默认装的是软链接。以后 `dongbei-explainer` 更新了，这边直接就能用，不用再复制一遍。

装完回到 Codex 或 Claude Code 的**聊天输入框**，直接说人话就行：

```text
用 dongbei-explainer 解释这个 issue。面向一般 STEM 读者，先讲问题怎么发生。
```

注意，这句话是发在聊天框里的，不是 CLI 命令。平时说“用东北大白话给我讲讲这个 PR”也行。“说清楚、说明白、讲透、仔细讲讲、从头捋一遍、通俗点、别绕、没看明白、这到底怎么回事”这些说法也应该触发。这里看的是用户真想把事情弄懂，不是死认几个关键词。

这个触发范围只管 agent 直接回复用户的解释。要是任务同时要求写 code、documentation、Git message、PR comment、issue、report、prompt、configuration 或 test，这些产物仍然保持任务要求的专业语言和风格，不能跟着变成东北话。除非用户明确要求某个产物也使用这种风格。

要是它没认出来，再在**聊天输入框**里点名。Codex 输入 `$dongbei-explainer 解释这个 issue`，Claude Code 输入 `/dongbei-explainer 解释这个 issue`。这俩前缀是兜底用的，不是每回都得写。

Claude Code 会监看启动时已经存在的 skill 目录；如果 `.claude/skills/` 是刚才才第一次创建的，重启一次 Claude Code，再回到聊天输入框使用它。这是 Claude Code [官方文档说明的加载边界](https://code.claude.com/docs/en/slash-commands#where-skills-live)。

Codex 会不会在已经运行的会话里立刻刷出新装的 skill，目前没有能核实的官方说明。先在聊天框里试。没认出来，就从同一个项目新开一个 Codex 会话，这么整最稳。

如果你现在就要用、不想重启，也可以直接让当前 agent 读取 canonical skill：

```text
请读取并使用
/path/to/dongbei-explainer/skills/dongbei-explainer/SKILL.md，
以及它要求组合的四个 sibling skills，然后解释下面的问题：……
```

这相当于只给眼前这个会话手动加载一次，不会永久安装。

### 不想每个项目都装一遍

那就装到个人目录。往后新开项目也能用：

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

## 网页聊天咋用

网页产品要是支持上传或安装 Agent Skills，把 `skills/` 下需要的目录加进去，然后直接问：

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

网页聊天不支持 Skills 也没啥。把相关 `SKILL.md` 和它链接的 reference 文件当附件传上去，再提问题就行。只想讲清楚，装 `clear-tech-explainer + plain-chinese`。想要完整效果，再加 `concrete-example + dongbei-voice`。

OpenAI 当前也把可重复工作流作为 Skills 使用场景；参见 [OpenAI Docs / ChatGPT use cases](https://learn.chatgpt.com/use-cases)。不同网页产品的上传入口会变化，所以这里不绑定某个按钮名称。

## 先不安装，试一把

把下面这段直接发给模型：

```text
用清楚、自然、带一点东北口语节奏的中文解释下面的问题。
目标读者有一般 STEM 背景，但不一定懂计算机，也不了解这个项目。
先说原来发生了什么，再说真正卡在哪儿、现在改了哪一步；
拿一个具体对象走完整个过程。保留必要的英文术语、代码和公式，
项目内部黑话第一次出现时先用中文说明它负责什么。
不要喜剧化，不要堆东北词，也别把读者当笨蛋。
```

临时这么用没问题。不过完整 skill 还管术语记忆、解释深度和反例，跑多轮对话会更稳。

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

## 五个 skill，各管一摊

| Skill | 负责什么 |
|---|---|
| `clear-tech-explainer` | 先把因果链、before/after、边界和 trade-off 搭对 |
| `plain-chinese` | 去掉名词堆和循环定义，按读者熟悉度处理术语 |
| `concrete-example` | 让一个 commit、request、tensor、数字或状态真走一遍 |
| `dongbei-voice` | 加入克制但能感知的东北口语节奏 |
| `dongbei-explainer` | 按顺序组合上面四层 |

为啥非得拆开？因为讲清楚和东北口吻不是一回事。你可以只让它把因果关系讲明白，一点东北味都不要；也可以把 `dongbei-voice` 接到别的解释流程上。非得揉成一个大 prompt，后面想调哪一层都费劲。具体怎么接的，见 [docs/architecture.md](docs/architecture.md)。

## 英文术语咋办

不乱翻，也不逮着一个词就给人上课。

- 标准英文术语保留英文；
- Tier 1 直接使用，不做 AI 教师式重复定义；
- Tier 2 在第一次真正需要时用一句话说明，后面直接复用；
- 项目自己发明的英文长标签不自动算标准术语，先用中文说它负责什么；
- 同一轮对话里已经解释过的词，不再从头讲一遍。

第一轮人工标了 223 个英文术语和 164 条中文表达。哪些词直接用，哪些词第一次得解释，结果都在 [technical jargon tiers](skills/plain-chinese/references/common-technical-jargon.md) 和 [expression boundary](skills/dongbei-voice/references/expression-boundaries.md)。这不是给全体普通话用户下定义。哪项标得不对，后面接着改。

## 这套东西校过吗

校过。词汇边界做过人工标注，完整回答也拿真实技术问题做过 A/B 对照，专门检查它有没有讲清机制、丢掉技术条件或者把东北话说成表演。

这不等于证明“东北话一定更好使”，只能说明这些 skills 不是凭感觉写完就算了。想看具体怎么测的，材料和 rubric 都在 [eval/](eval/README.md)，阶段二标注页在 [eval/phase2/](eval/phase2/README.md)。

## 目前研究到哪儿了

目前看，真正管用的多半不是那些特别地方的词，而是把动作说出来、把状态说具体、用短问短答带着人往下走。语言研究在 [research/dongbei-language-notes.md](research/dongbei-language-notes.md)，小品和访谈只提炼结构，不转载全文，也不能改掉人工标过的词汇边界。语料笔记放在 [research/corpus/](research/corpus/README.md)。

还是那句话，咱没证明东北话能提高 LLM reasoning。现在能说的只有：

> 实际用起来，这种说法经常能把模型从空话里拽出来，让它多讲具体动作和因果。到底能好多少，得接着测。

## 怎么参与

```bash
scripts/validate
scripts/validate_phase2 eval/phase2/bundles/<bundle>.json
scripts/lint_text path/to/answer.md
```

哪句东北话让普通话用户看懵了，哪个类比把技术机制讲歪了，或者哪个回答看着顺却偷偷丢了条件，都欢迎提。真实 case 尤其有用。Codex、Claude Code 和其他 agent 跑出来不一样，也可以把对照结果交上来。

怎么交见 [CONTRIBUTING.md](CONTRIBUTING.md)。代码和 skills 用 [MIT License](LICENSE)。
