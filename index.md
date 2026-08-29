# llm-wiki-tags index

Agent-facing index for this repository. llm-wiki-tags is the same **llm-wiki**
([gist by Andrej Karpathy](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)),
plus **tags**.

The convention itself is **not applied here**: it is for repositories whose main
subject is code, with documentation serving the code. This repo has no code —
it is the instruction and the rule files an agent installs elsewhere. Every
directory still carries an `index.md`, because that is plain navigation.

## Files

- [`README.md`](README.md) — English description: what llm-wiki-tags is, the tag
  format, search commands and the `index.md` rules.
- [`README.ru.md`](README.ru.md) — Russian description (same content).
- [`INSTRUCTIONS.md`](INSTRUCTIONS.md) — English agent install instructions; the
  page to point an agent at ("install <url>").
- [`INSTRUCTIONS.ru.md`](INSTRUCTIONS.ru.md) — Russian agent install instructions
  ("поставь <url>").
- [`RELEASE-NOTES.md`](RELEASE-NOTES.md) — what changed in each version
  (English).
- [`RELEASE-NOTES.ru.md`](RELEASE-NOTES.ru.md) — the same in Russian.
- [`LICENSE`](LICENSE) — public-domain dedication (The Unlicense).

## Directories

- [`rules/`](rules/index.md) — the rule files an installing agent copies into a
  target repository as `.claude/rules/llm-wiki-tags/`; the canonical wording of
  the convention (English and Russian).
- [`languages/`](languages/index.md) — per-language rules for placing `@tag:`
  tokens in code (Java, Python, Go), in prose.

## Where to start

- Humans: read [`README.md`](README.md) / [`README.ru.md`](README.ru.md).
- Agents asked to install it: follow [`INSTRUCTIONS.md`](INSTRUCTIONS.md) /
  [`INSTRUCTIONS.ru.md`](INSTRUCTIONS.ru.md).
- Agents editing this repository: read [`AGENTS.md`](AGENTS.md).

## Tags

This repo defines the tag mechanism but is documentation-only, so it registers no
tags of its own. A repository that installs llm-wiki-tags keeps its tag registry
in `docs/tags.md`.
