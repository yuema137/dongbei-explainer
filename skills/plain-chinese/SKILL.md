---
name: plain-chinese
description: Rewrite or draft Chinese technical prose with fewer abstract noun piles, circular definitions, unexplained acronyms, and vague relationship claims. Use independently for plain technical Chinese; preserves established English jargon according to audience familiarity.
license: MIT
---

# Plain Chinese

Reduce prose burden without reducing technical content.

Replace abstract subjects with actors and actions. Turn named relationships into visible consequences. Break long qualification chains. When a sentence says a framework “enables” something, state what sends, stores, waits, calls, or changes.

Apply an aloud test to the Chinese around necessary jargon: would a technically competent person naturally say this sentence to a colleague? Rewrite compressed inventions such as “同步强杀”, “语义闭包”, “能力外置”, or “执行态持久化” unless they are exact source terms that the reader must recognize. Short four-character compounds are not automatically plain language. Prefer ordinary clauses: “不是一调用就立刻停掉”, “把这条规则从代码里拿出来，让配置传进来”, “先把结果写到 watchdog 能读到的文件里”.

Necessary jargon may remain as an exact island inside an otherwise natural sentence. Do not make every word around it sound like documentation.

Apply the audience-aware terminology contract in [references/terminology-policy.md](references/terminology-policy.md). When a concrete term needs classification, consult the human-calibrated [references/common-technical-jargon.md](references/common-technical-jargon.md). Preserve established English terms; this is not a jargon-translation system.

During revision, flag:

- three or more abstract nouns carrying the sentence;
- definitions that use an unexplained synonym;
- acronyms used before their meaning matters;
- relationship labels without operational consequences;
- repeated first-use definitions;
- filler transitions and teacherly restatement.
- Chinese that is grammatically valid but nobody would normally say aloud.

Keep the user's requested precision and length. Do not turn every answer into a lesson.

For representative rewrites, read [references/jargon-rewrites.md](references/jargon-rewrites.md).
