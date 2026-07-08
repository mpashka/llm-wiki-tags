# Placing tags in Java code

*Languages: **English** · [Русский](java.ru.md) — Parent: [languages index](index.md)*

A tag is the `@tag:<slug>` token inside a comment placed immediately above the
element it marks. Any comment style works — line (`//`), block (`/* */`) or
Javadoc (`/** */`). Prefer Javadoc where the element already has documentation, so
the tag travels with the API docs. Multiple tags are space-separated
(`@tag:payments @tag:retry`).

## Granularity

- **Package** — in `package-info.java`, in the Javadoc above the `package`
  declaration:
  ```java
  /**
   * Payments domain.
   * @tag:payments
   */
  package com.example.payments;
  ```

- **File** — a comment at the very top of the `.java` file, above the `package`
  line and imports:
  ```java
  // @tag:payments
  package com.example.payments;
  ```

- **Class** (also interface, enum, record) — a comment directly above the
  declaration:
  ```java
  /** Charges a card. @tag:payments @tag:retry */
  public class ChargeService { ... }
  ```

- **Method** — a comment directly above the method:
  ```java
  // @tag:retry
  public void charge(Card card) { ... }
  ```
