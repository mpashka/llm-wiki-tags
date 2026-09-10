# Rule files to install

*Languages: **English** · [Русский](index.ru.md) — Parent: [repository index](../index.md)*

Ready-made rule files. An agent installing llm-wiki-tags copies them into the
target repository as `.claude/rules/llm-wiki-tags/` — see step 1 of
[`INSTRUCTIONS.md`](../INSTRUCTIONS.md). They are the **canonical wording** of the
convention: `README.md` describes it, these files state it as rules.

Claude Code loads every `.md` under a project's `.claude/rules/` on each task. A
file whose front matter has a `paths:` field is loaded **only** when a matching
file is touched, which is how the per-language rules stay out of the way until
they apply. `paths:` takes a list or a comma-separated string with brace
expansion (`paths: "**/*.ts, **/*.tsx"`).

## Files

Always loaded:

- [`wiki.md`](wiki.md) — the `index.md` tree, read before you act, update as you go.
- [`docs-layout.md`](docs-layout.md) — the `docs/` tree: specification,
  implementation, testing, requests.
- [`tags.md`](tags.md) — tag format, hierarchy, the `docs/tags.md` registry,
  search commands.
- [`glossary.md`](glossary.md) — the `docs/terms.md` glossary: search by meaning
  before naming, one definition per term, synonyms point to the main term.

Loaded per language (copy only the ones the repository uses):

- [`code-tags-java.md`](code-tags-java.md) — `paths: ["**/*.java"]`.
- [`code-tags-python.md`](code-tags-python.md) — `paths: ["**/*.py"]`.
- [`code-tags-golang.md`](code-tags-golang.md) — `paths: ["**/*.go"]`.

Each file has a `.ru.md` twin with the same content in Russian; install one
language, dropping `.ru` from the file name. Cross-links inside the files use the
installed names (`wiki.md`, `docs-layout.md`, `tags.md`), so they resolve after
the copy without editing.

For a language without a `code-tags-*.md` file, write one from
[`languages/`](../languages/index.md), which covers the same ground in prose.

Do not copy this index into the target repository — it belongs to this repo, and
under `.claude/rules/` it would be loaded as a rule.
