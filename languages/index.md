# Tag placement by language

*Languages: **English** · [Русский](index.ru.md) — Parent: [repository index](../index.md)*

Per-language rules for where to place `@tag:<slug>` tokens **in code**. In every
language a tag can mark four granularities — a **package**, a **file**, a
**class** (or its equivalent) and a **method/function** — always written as the
`@tag:<slug>` token inside a comment in the language's syntax, placed immediately
above the element it marks.

For the overall mechanism and for **documentation** tagging (YAML front matter,
`index.md`, body tags) see [`INSTRUCTIONS.md`](../INSTRUCTIONS.md) /
[`INSTRUCTIONS.ru.md`](../INSTRUCTIONS.ru.md) and [`README.md`](../README.md).

## Files

- [`java.md`](java.md) — tags in Java (`//`, `/* */`, Javadoc; `package-info.java`).
- [`python.md`](python.md) — tags in Python (`#` comments and docstrings; `__init__.py`).
- [`golang.md`](golang.md) — tags in Go (`//` doc comments; `doc.go`).

For a language not listed, apply the same idea: the `@tag:<slug>` token in a
comment (in that language's comment syntax) directly above the package, file,
class-equivalent or function it marks.
