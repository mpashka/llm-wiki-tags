# Placing tags in Go code

*Languages: **English** · [Русский](golang.ru.md) — Parent: [languages index](index.md)*

A tag is the `@tag:<slug>` token inside a `//` comment (or `/* */`) placed
immediately above the element. Prefer the element's doc comment, so the tag lives
with `go doc` output. Go has no classes — the class-level granularity maps to a
**type** (struct/interface). Multiple tags are space-separated
(`@tag:payments @tag:retry`).

## Granularity

- **Package** — in the package doc comment above the `package` clause; for a
  package spanning several files use a dedicated `doc.go`:
  ```go
  // Package payments handles charging.
  // @tag:payments
  package payments
  ```

- **File** — a `//` comment at the top of the `.go` file. Note: a comment directly
  above `package` is the *package* doc comment; for a file-scoped tag put it on the
  file's first declaration instead.

- **Type** (struct / interface) — a comment directly above the `type`:
  ```go
  // ChargeService charges a card. @tag:payments
  type ChargeService struct{ ... }
  ```

- **Function / method** — a comment directly above `func`:
  ```go
  // @tag:retry
  func (s *ChargeService) Charge(c Card) error { ... }
  ```
