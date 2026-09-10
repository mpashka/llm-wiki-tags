---
description: "One concept, one word: the docs/terms.md glossary — search by meaning before naming, one definition per term, synonyms point to the main term."
---

# llm-wiki-tags — glossary

"One concept — one word" holds not only in code but in the docs, in task
statements and in conversation. The glossary is what keeps it: without one, every
session names a concept its own way, and the next session takes the new name for
a new concept and creates a second one. Companion rules: [`wiki.md`](wiki.md),
[`docs-layout.md`](docs-layout.md), [`tags.md`](tags.md).

## Format

The glossary is `docs/terms.md`, one entry per concept:

```
- **retry budget** (retry quota, retry limit) — how many retries a payment may
  spend before it is failed. See [payments/retry](implementation/payments/retry.md).
```

- The **main term** in bold; in parentheses, the synonyms it replaces; then a
  one-to-three-line definition and a link to the page that owns the concept. The
  glossary defines; how the thing works is on the owning page.
- **Jargon** goes in its own section, each entry naming the main term to write
  instead.
- **Resolved ambiguities** close the file: a word that was used for two concepts,
  and which one it means now — so the question is not reopened.

## Rules

1. **Search before you name.** A new name — in code, a doc, a task statement or an
   issue — is introduced only after searching the glossary **by meaning, not by
   word**: definitions and synonyms. Found under another name: use the main term
   and add the name you heard to its synonyms.
2. **A new name for an old concept becomes a synonym** in the same change,
   wherever it came from — an issue, a colleague, someone else's docs. Quotations
   stay verbatim; your own text uses the main term.
3. **A term is defined once.** A second definition of the same concept is a defect
   even when it is worded differently: two definitions drift apart silently.
4. **Levels.** A repository's glossary owns its terms. A glossary shared by several
   repositories holds only what they have in common, the name normalisation and a
   list of the repository glossaries; it links to a repository's definition
   instead of copying it.
5. **Term, tag and code name are one concept.** A cross-cutting concept gets both
   a term and a tag: the definition lives in the glossary, and `docs/tags.md`
   links to it. A class that names a domain entity uses the main term. Code
   vocabulary — which suffix means what (`Manager` vs `Service`) — is a naming
   guide, not the glossary.
