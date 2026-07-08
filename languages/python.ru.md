# Простановка тэгов в коде Python

*Языки: [English](python.md) · **Русский** — Родитель: [индекс языков](index.ru.md)*

Тэг — это токен `@tag:<slug>` внутри `#`-комментария прямо над элементом либо
внутри docstring элемента. Несколько тэгов — через пробел
(`@tag:payments @tag:retry`).

## Уровни

- **Пакет** — в `__init__.py` пакета, комментарием в начале файла или в docstring
  модуля:
  ```python
  # @tag:payments
  ```

- **Модуль / файл** — `#`-комментарий в начале `.py`-файла (ниже возможного
  `from __future__`) либо docstring модуля:
  ```python
  """Payments domain. @tag:payments"""
  ```

- **Класс** — комментарий прямо над `class` либо его docstring:
  ```python
  # @tag:payments
  class ChargeService:
      """Charges a card. @tag:retry"""
  ```

- **Функция / метод** — комментарий прямо над `def` либо его docstring:
  ```python
  # @tag:retry
  def charge(card): ...
  ```
