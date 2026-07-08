# Placing tags in Python code

*Languages: **English** · [Русский](python.ru.md) — Parent: [languages index](index.md)*

A tag is the `@tag:<slug>` token inside a `#` comment placed immediately above the
element, or inside the element's docstring. Multiple tags are space-separated
(`@tag:payments @tag:retry`).

## Granularity

- **Package** — in the package's `__init__.py`, a top-of-file comment or the
  module docstring:
  ```python
  # @tag:payments
  ```

- **Module / file** — a `#` comment near the top of the `.py` file (below any
  `from __future__` import), or the module docstring:
  ```python
  """Payments domain. @tag:payments"""
  ```

- **Class** — a comment directly above `class`, or its docstring:
  ```python
  # @tag:payments
  class ChargeService:
      """Charges a card. @tag:retry"""
  ```

- **Function / method** — a comment directly above `def`, or its docstring:
  ```python
  # @tag:retry
  def charge(card): ...
  ```
