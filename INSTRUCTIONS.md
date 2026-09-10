# Install llm-wiki-tags (agent instructions)

> # llm-wiki-tags IS THE SAME **llm-wiki** BY ANDREJ KARPATHY — WITH **TAGS**.

*Languages: **English** · [Русский](INSTRUCTIONS.ru.md) — About:
[English](README.md) · [Русский](README.ru.md)*

You are an AI coding agent. The user asked you to **install llm-wiki-tags** into
the current repository. Follow the steps below, adapting paths and comment syntax
to the repo. Do not restructure or rewrite existing content beyond what is needed
to satisfy these rules. Make the changes as a normal edit to the repo.

## Concept

Keep the docs as an LLM-readable wiki (llm-wiki —
[original gist by Andrej Karpathy](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)),
and add **tags** that link code and documentation across the directory tree.

A **tag** is a short kebab-case slug (`[a-z0-9-]+`, hierarchical with `/`)
written as the token `@tag:<slug>`. The **same tag is placed in both code and
documentation**, so a concept spanning several files/folders is reachable in one
search.

The convention ships as **rule files**. You install them into the repository
first (step 1) and then apply them — the rules are the canonical wording, this
page is only the procedure.

## Steps

### 1. Install the rule files

Copy the files from [`rules/`](rules/index.md) into
`.claude/rules/llm-wiki-tags/` **verbatim** — do not paraphrase them. Claude Code
loads every `.md` under `.claude/rules/` on each task, which is what makes the
convention stick. Fetch them from
`https://raw.githubusercontent.com/mpashka/llm-wiki-tags/main/rules/<file>`.

Always:

| Source | Install as |
| --- | --- |
| `rules/wiki.md` | `.claude/rules/llm-wiki-tags/wiki.md` |
| `rules/docs-layout.md` | `.claude/rules/llm-wiki-tags/docs-layout.md` |
| `rules/tags.md` | `.claude/rules/llm-wiki-tags/tags.md` |
| `rules/glossary.md` | `.claude/rules/llm-wiki-tags/glossary.md` |

Plus one `code-tags-<lang>.md` per language the repository actually uses —
`rules/code-tags-java.md`, `code-tags-python.md`, `code-tags-golang.md` — and
none for languages it does not. Each carries a `paths:` field in its front
matter, so it is loaded only when a file of that language is touched.

- **Language of the rules**: each file has a `.ru.md` twin. Install the twin that
  matches the language of the repository's documentation, dropping `.ru` from the
  installed file name.
- **A language with no ready file**: write one after the same pattern from
  [`languages/`](languages/index.md), with the right `paths:` glob
  (`paths: "**/*.ts, **/*.tsx"` — a list or a comma-separated string).
- **Adapt after copying, not instead of it**: if the repo's docs directory is not
  `docs/`, or a rule genuinely does not fit, edit the installed file and say so in
  your report.

Now read what you installed and apply it in the steps below.

### 2. Lay out the documentation — `docs-layout.md`

Create the `docs/` tree: `specification/` (the outside view), `implementation/`
(the inside view), `testing/`, `requests/` (per-task working files). Move stray
docs out of the repository root into it, fixing the links; leave a page at the
root only when tooling or an external URL requires it. Keep an existing docs
directory's name if the repo already has one.

### 3. Establish the `index.md` tree — `wiki.md`

Ensure every meaningful directory — under `docs/` and in the code tree alike —
has an `index.md` with a one-line description of each file and sub-directory in
it, linking to its parent index and its child indexes. Create the missing ones.

### 4. Create the tag registry — `tags.md`

Create `docs/tags.md`: every tag with a one-line description of the concept it
links, laid out hierarchically, plus the tag format and the search commands
(copy the "Tag format" and "Searching" sections from [`README.md`](README.md)).
Add it to `docs/index.md`.

### 5. Create the glossary — `glossary.md`

Create `docs/terms.md` and add it to `docs/index.md`. Seed it with the domain
terms that already recur in the code and docs — class and module names, words
from the existing pages — each with its main term, the synonyms in use and a
one-line definition. Where one concept goes by two names, take the one the code
already uses as the main term and record the other as a synonym; do not rename
code in this step. Do not invent terms the repository does not use.

### 6. Place tags — `tags.md`, `code-tags-<lang>.md`

For each concept that spans **both code and docs**: choose a slug, register it in
`docs/tags.md`, then put the literal `@tag:<slug>` token in the docs (YAML front
matter, or a body line for a single section) and in the code (a comment above the
package, file, class or function). Prefer hierarchy — `@tag:payments/retry` —
over long flat slugs, and do not invent tags for one-off details.

### 7. Record the convention for other agents

Agents other than Claude Code do not read `.claude/rules/`. In the repository's
agent guide (`AGENTS.md`, else create it), add a short **"llm-wiki-tags"**
section: five or six lines summarising the installed rules, plus links to
`.claude/rules/llm-wiki-tags/`, `docs/tags.md` and `docs/terms.md`. Keep the
detail in the rule files — the guide points at them, it does not duplicate them.

## In brief (the canonical wording is in the rule files)

- **Documentation is an LLM wiki**: an `index.md` per meaningful directory,
  bidirectional links, one page owns each detail.
- **All docs live under `docs/`** — `specification/`, `implementation/`,
  `testing/`, organised by tag and hierarchical where possible; the root keeps
  only the files that must be there.
- **Task working files go to `docs/requests/<task_name>/`** (`request.md`,
  `plan.md`, debug scripts) — not to the root, not next to the code.
- **Read before you act; update as you go.** Documentation that no longer matches
  the code is a defect.
- **Tag cross-cutting concepts** and keep `docs/tags.md` current.
- **One concept — one word**: search `docs/terms.md` by meaning before naming
  anything; a new name for an old concept becomes a synonym.

## Done

After installing, tell the user what you created/changed: the rule files under
`.claude/rules/llm-wiki-tags/` (and which languages), the `docs/` layout, the
`index.md` files added, `docs/tags.md`, `docs/terms.md` and the terms seeded, any
tags placed, and the agent-guide section. From now on, follow the installed rules on every task in this
repository.
