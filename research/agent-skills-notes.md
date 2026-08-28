# Agent Skills portability notes

Checked 2026-08-28. These notes describe the design inputs, not a promise that host paths never change.

## Common standard

The [Agent Skills specification](https://agentskills.io/specification) requires one directory per skill and a `SKILL.md` containing YAML frontmatter plus Markdown. `name` and `description` are required; `scripts/`, `references/`, and `assets/` are optional. The standard explicitly describes progressive disclosure: hosts discover metadata first, load the body on activation, and load linked resources only when needed.

Canonical files therefore use only the common subset: `name`, `description`, `license`, Markdown, relative references, and ordinary files. They do not use dynamic shell injection, host-specific invocation flags, subagent frontmatter, or vendor state APIs.

## Host adapters

- [Claude Code documentation](https://code.claude.com/docs/en/slash-commands#where-skills-live) lists `.claude/skills/<name>/SKILL.md` for project skills and `~/.claude/skills/<name>/SKILL.md` for personal skills. It also documents additional Claude-only frontmatter and dynamic context injection; canonical skills intentionally avoid these.
- OpenAI's current Skills guidance describes skills as portable Agent Skills bundles. Local Codex conventions in the current environment discover personal skills under `~/.agents/skills`; the installer treats the path as an adapter, not part of skill semantics.

Host paths can evolve. `scripts/install` keeps them isolated and offers a destination override.

## Architectural decision

`skills/` is the only source of truth. `.agents/skills/` and `.claude/skills/` are generated installation targets and are not committed. There are no Codex and Claude behavior forks.
