# Простановка тэгов в коде Java

*Языки: [English](java.md) · **Русский** — Родитель: [индекс языков](index.ru.md)*

Тэг — это токен `@tag:<slug>` внутри комментария, поставленного прямо над
маркируемым элементом. Подходит любой стиль комментария — строчный (`//`),
блочный (`/* */`) или Javadoc (`/** */`). Там, где у элемента уже есть Javadoc,
ставь тэг в него, чтобы тэг шёл вместе с документацией API. Несколько тэгов — через
пробел (`@tag:payments @tag:retry`).

## Уровни

- **Пакет** — в `package-info.java`, в Javadoc над объявлением `package`:
  ```java
  /**
   * Payments domain.
   * @tag:payments
   */
  package com.example.payments;
  ```

- **Файл** — комментарий в самом верху `.java`-файла, над строкой `package` и
  импортами:
  ```java
  // @tag:payments
  package com.example.payments;
  ```

- **Класс** (а также интерфейс, enum, record) — комментарий прямо над объявлением:
  ```java
  /** Charges a card. @tag:payments @tag:retry */
  public class ChargeService { ... }
  ```

- **Метод** — комментарий прямо над методом:
  ```java
  // @tag:retry
  public void charge(Card card) { ... }
  ```
