# llm-wiki-plus index

Agent-facing index for this repository. llm-wiki-plus is the same **llm-wiki**
([gist by Andrej Karpathy](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)),
plus **tags**. This repo eats its own dogfood: every meaningful
directory carries an `index.md` (there is one directory — the root).

## Files

- [`README.md`](README.md) — English description: what llm-wiki-plus is, the tag
  format, search commands and the `index.md` rules.
- [`README.ru.md`](README.ru.md) — Russian description (same content).
- [`INSTRUCTIONS.md`](INSTRUCTIONS.md) — English agent install instructions; the
  page to point an agent at ("install <url>").
- [`INSTRUCTIONS.ru.md`](INSTRUCTIONS.ru.md) — Russian agent install instructions
  ("поставь <url>").
- [`LICENSE`](LICENSE) — public-domain dedication (The Unlicense).

## Where to start

- Humans: read [`README.md`](README.md) / [`README.ru.md`](README.ru.md).
- Agents asked to install it: follow [`INSTRUCTIONS.md`](INSTRUCTIONS.md) /
  [`INSTRUCTIONS.ru.md`](INSTRUCTIONS.ru.md).

## Tags

This repo defines the tag mechanism but is documentation-only, so it registers no
tags of its own. A repository that installs llm-wiki-plus keeps its tag registry
in `docs/tags.md`.
