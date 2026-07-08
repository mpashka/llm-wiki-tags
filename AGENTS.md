# AGENTS.md

This file provides guidance to AI coding agents when working with code in this
repository. (`CLAUDE.md` points here.)

## Tooling

**Use the IntelliJ IDEA MCP (`mcp__idea__*`) for working with code and files** in
this repository — reading (`mcp__idea__read_file`), searching
(`mcp__idea__search_text` / `search_regex`), and editing
(`mcp__idea__apply_patch` / `create_new_file`) — in preference to raw shell
(`cat`, `sed`, `grep`) so edits go through the IDE and pick up its
reformatting/linting.

## What this repo is

This is a **documentation-only** repository. It has no source code, build, tests,
or lint — it *specifies a convention* called **llm-wiki-tags** and ships the docs
that describe and install it. There is nothing to compile or run; work here means
editing Markdown.

The convention: llm-wiki (Andrej Karpathy's idea of a codebase's docs kept as an
LLM-readable wiki of `index.md` files) **plus tags** — `@tag:<slug>` tokens placed
in *both* code and docs to link cross-cutting concepts across the directory tree.

## Files

- `README.md` / `README.ru.md` — human-facing description (English / Russian).
- `INSTRUCTIONS.md` / `INSTRUCTIONS.ru.md` — the payload: agent instructions a
  user points their coding agent at ("install <url>") to set up the convention in
  *another* repo. This is the primary product.
- `index.md` — the repo's own llm-wiki index (this repo eats its own dogfood).
  English-only (there is no `index.ru.md`).
- `languages/` — per-language rules (`java.md`, `python.md`, `golang.md`, each with
  a `.ru.md` twin) for where to place `@tag:` tokens in code, plus its own
  `index.md` / `index.ru.md`.
- `LICENSE` — The Unlicense (public domain).

The content `.md` files come in mirrored English/Russian pairs. **Any change to content
in one language must be mirrored in its `.ru`/`.md` counterpart** so the pairs
stay in sync.

## Editing rules (this repo follows its own convention)

- **Keep `index.md` current.** If you add, remove, rename, or repurpose a file,
  update the one-line description for it in `index.md` in the same change.
- **Content is duplicated across three surfaces by design**: the tag format and
  search commands appear in the READMEs, the INSTRUCTIONS, and (in an installed
  repo) `docs/tags.md`. When editing the canonical wording (tag format, the
  `index.md` rules, search commands), change all matching copies together.
- This repo registers **no tags of its own** — it is documentation-only. Do not
  add a `docs/tags.md` here; that file is what INSTRUCTIONS tells agents to create
  in *installing* repos.

## The convention itself (for reference)

A tag is a lowercase kebab-case slug (`[a-z0-9-]+`) written as the `@tag:<slug>`
token. In **docs** it goes in YAML front matter (`tags: "@tag:x @tag:y"`) at the
top of the `.md` — for a directory, its `index.md` — or as a body line for a
single section. In **code** it goes in a leading comment (`// @tag:x`, `# @tag:x`,
`/* @tag:x */`) above a package, file, class or method (see `languages/`). The
literal token is kept in both so one grep spans code and docs. Search:

```bash
grep -rn "@tag:<slug>" .                     # all locations of a tag
grep -oE "@tag:[a-z0-9-]+" path/to/file      # tags on a file
grep -rhoE "@tag:[a-z0-9-]+" . | sort -u     # all tags in the repo
```
