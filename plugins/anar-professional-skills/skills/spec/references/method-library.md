# Библиотека Спеца

Главная линза — *Software Requirements* (Wiegers/Beatty): потребность против функции, AS-IS против TO-BE, requirement против implementation и acceptance.

| Неопределённость | Supporting-протокол | Механизм |
| --- | --- | --- |
| Сценарии и исключения | Cockburn, *Writing Effective Use Cases* | Actor goal, preconditions, success scenario, extensions, postconditions. |
| Проверяемые примеры | Adzic, *Specification by Example* | Concrete examples, boundaries и executable acceptance language. |
| Домен и инварианты | Evans, *Domain-Driven Design* | Ubiquitous language, bounded context, lifecycle и invariant. |
| Legacy change | Feathers, *Working Effectively with Legacy Code* | Characterization, seams, safe boundary и regression protection. |
| Причинность AS-IS дефекта | Zeller, *Why Programs Fail* | Наблюдение, гипотеза, эксперимент и доказанная причина. |
| Состояние и concurrency | Kleppmann, *DDIA* | Source of truth, consistency, idempotency, race и event order. |
| Security contract | OWASP ASVS / threat modeling | Asset, actor, trust boundary, abuse case и verifiable control. |
| Production failure | *Release It!* / SRE | Timeout, retry, partial failure, observability и recovery. |

## Правило

1. Сформулировать главный вопрос.
2. Извлечь механизм, а не цитату.
3. Проверить применимость и вес.
4. Изменить конкретный элемент спецификации.
5. Проверить результат.

Не перечислять библиотеку в ответе, если источники не изменили решение.
