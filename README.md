# dongbei-explainer

> 东北话不是目的。讲明白才是目的。

`dongbei-explainer` is a portable Agent Skills toolkit for clear Chinese technical explanation. Its working hypothesis is deliberately modest: a light Northeastern conversational rhythm may push an explanation toward concrete actions, short causal turns, and explicit before/after structure. The project turns that observation into separable skills and calibration material.

This is **not** a dialect role-play pack, comedy prompt, jargon translator, or claim that Northeastern Mandarin improves model reasoning. Technical correctness stays first.

## What changes in an explanation

Dense technical prose:

> Dependency inversion introduces abstractions to decouple high-level modules from concrete implementations.

Clear core:

> 原来订单代码里直接写死“调用 Stripe”。换支付渠道时，订单代码也得改。`dependency inversion` 改的是依赖方向：订单代码只声明“我需要一个能收费的对象”；具体渠道来实现这个接口。

Full, restrained voice:

> 先看原来卡在哪儿：订单代码直接去找 Stripe，Stripe 一换，订单代码也跟着动。`dependency inversion` 干的事，是让订单代码别认具体厂商，只认“能收费”这个接口。说白了，它拆掉的是这根写死的线，不是让依赖凭空没了；接口和适配器照样得维护。

The last version does not merely add `整` or `啥`; it changes pacing and emphasis while retaining cost and mechanism.

## Layered architecture

| Skill | Independent job |
|---|---|
| `clear-tech-explainer` | causal explanation plan, depth control, correctness and preservation |
| `plain-chinese` | remove prose burden; preserve English terms using audience familiarity |
| `concrete-example` | add a small data/control/state trace when it helps |
| `dongbei-voice` | apply a conservative, cross-region-readable conversational rhythm |
| `dongbei-explainer` | compose all four in that order |

The semantic method and surface voice are separate. Use any combination:

- “用 `clear-tech-explainer` 解释 rebase。”
- “再加 `concrete-example`，画 commit graph。”
- “只把这段用 `plain-chinese` 改清楚。”
- “保持原工作流，加一点 `dongbei-voice`。”
- “用完整 `dongbei-explainer`，level 3。”

See [architecture](docs/architecture.md) for the composition contract.

## One canonical interface

`skills/` is the only source of truth and stays inside the open [Agent Skills specification](https://agentskills.io/specification). Host differences are installation differences, not behavior forks.

Project install using symlinks:

```bash
scripts/install codex
scripts/install claude-code
```

Personal install:

```bash
scripts/install codex --scope user
scripts/install claude-code --scope user
```

Use `--copy` when symlinks are undesirable, or `--dest PATH` if current host documentation specifies another discovery path. The installer refuses to overwrite an existing skill. Current source research is recorded in [Agent Skills notes](research/agent-skills-notes.md).

## Terminology: familiarity, not translation

Established terms stay in English. Tier 1 terms are used directly; Tier 2 terms get one short explanation on first meaningful use; specialist terms get only the detail needed for the current argument. A term already explained in the conversation is reused without another parenthetical lesson.

These boundaries need human data. The no-dependency [card annotation UI](annotation/index.html) contains a large candidate pool for both English terminology and Dongbei expressions. Open it directly, label cards, and export JSON. The pools are deliberately broader than the recommended vocabulary and are not themselves policy.

## Language research

Initial sources support a conservative result: Northeastern Mandarin is close to Standard Mandarin; useful features include oral rhythm and vivid state/action description, while younger speakers' actual output often trends toward Standard Mandarin. That points to mostly Standard Mandarin plus explicit causal syntax, not a large local lexicon.

The [research table](research/dongbei-language-notes.md) separates preferred, sparing, and excluded expressions. `老铁`, `嘎嘎`, `咱就是说`, obscure local vocabulary, fake relatives, and phonetic misspellings are explicitly rejected. Expressions such as `咋`, `啥`, and `整` remain candidates for human calibration, not blanket recommendations.

## Calibration

The suite includes 16 single-turn cases across software, systems, ML, and statistics, plus six multi-turn conversations for terminology memory and depth changes. Each case specifies audience, required ideas, misconceptions, preserved details, and jargon decisions. There is no exact golden answer.

The [rubric](eval/rubric.md) separates correctness, causal clarity, concrete understanding, jargon burden, concision, accessibility, naturalness, restraint, respect, and information preservation. [Side-by-side variants](eval/samples/comparisons.md) compare default, plain, concrete, Dongbei, and full versions.

Calibration already changed the design:

- a KV-cache voice draft lost remaining attention cost, so voice now runs last with a preservation check;
- `整` hid exact systems operations, so precise verbs take precedence;
- a merge/rebase analogy hid commit identity, so the example became a commit graph;
- the offset case showed that expert answers must reach the equation quickly;
- comparisons showed plain language provides most of the gain; Dongbei voice mainly improves rhythm, so the layers remain independent.

Full notes: [initial calibration findings](eval/calibration-findings.md).

## Validation

```bash
scripts/validate
python3 /path/to/skill-creator/scripts/quick_validate.py skills/clear-tech-explainer
scripts/lint_text path/to/generated-answer.md
```

The repository validator checks metadata, local Markdown links, case count when PyYAML is available, and duplicate annotation candidates. The standard validator should be run on all five skills. The dialect linter catches explicit exclusions and warns on density; it does not replace human judgment.

## Limitations and contributions

There is not yet a public, representative corpus that justifies quantitative claims about cross-region comprehension of each expression. Live cross-host behavior has not yet been measured. The initial comparison is curated self-review, not a blinded experiment.

Contributions should add evidence, cases, or labeled judgments—not dialect density. See [CONTRIBUTING.md](CONTRIBUTING.md). MIT was chosen so skills and supporting material can be reused and adapted with minimal restriction; attribution and the license notice remain required.
