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
- `rules/` — the second half of the payload: ready-made rule files that an
  installing agent copies **verbatim** into a target repo as
  `.claude/rules/llm-wiki-tags/` (`wiki.md`, `docs-layout.md`, `tags.md`, and
  `code-tags-java|python|golang.md` carrying a `paths:` glob), each with a
  `.ru.md` twin, plus its own `index.md` / `index.ru.md`. **This is the canonical
  wording of the convention** — the READMEs describe it, these files state it.
- `index.md` — the repo's own navigation index. English-only (there is no
  `index.ru.md`).
- `languages/` — per-language rules (`java.md`, `python.md`, `golang.md`, each with
  a `.ru.md` twin) for where to place `@tag:` tokens in code, in prose, plus its
  own `index.md` / `index.ru.md`. They are the source the `code-tags-*.md` rules
  condense, and the reference for a language with no ready rule file.
- `RELEASE-NOTES.md` / `RELEASE-NOTES.ru.md` — what changed in each version.
  Add an entry when the convention changes, not for every edit.
- `LICENSE` — The Unlicense (public domain).

The content `.md` files come in mirrored English/Russian pairs. **Any change to content
in one language must be mirrored in its `.ru`/`.md` counterpart** so the pairs
stay in sync.

## llm-wiki-tags is not applied to this repo

The convention targets repositories **whose subject is code**, where the docs
exist to make the code understandable. This repo has no code, so it does not
install its own rules: there is no `.claude/rules/`, no `docs/` tree and no tag
registry here. `index.md` files stay as plain navigation. Do not "dogfood" the
convention here — a `docs/tags.md` or a `docs/specification/` in this repo would
be noise.

## Editing rules

- **Keep `index.md` current.** If you add, remove, rename, or repurpose a file,
  update the one-line description for it in `index.md` (and in
  `rules/index.md` / `languages/index.md`) in the same change.
- **`rules/` owns the wording of the convention.** The READMEs describe it for
  humans and `INSTRUCTIONS*` gives the procedure, but the normative text lives in
  `rules/`. When the tag format, the docs layout, the index rules or the search
  commands change, update `rules/*` first, then the matching passages in
  `README*.md` — and never let `INSTRUCTIONS*` grow its own paraphrase.
- `.claude/rules/` (in an *installing* repo) accepts `description:` and `paths:`
  in front matter; a file with `paths:` is loaded only when a matching file is
  touched. Verified against Claude Code 2.1.251 — the key is `paths:`, not
  `globs:`, and it takes a list or a comma-separated string.
