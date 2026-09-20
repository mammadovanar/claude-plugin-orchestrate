# Evidence и Loop-контракты

## Evidence

Для AS-IS использовать:

- `CONFIRMED BY USER | CODE | UI | API | DB | DOCUMENTATION`;
- `INFERRED FROM STRUCTURE | FLOW`;
- `UNKNOWN`.

Confidence:

- `HIGH` — непосредственно подтверждено;
- `MEDIUM` — устойчивый вывод из нескольких фактов;
- `LOW` — рабочая гипотеза;
- `UNKNOWN` — данных недостаточно.

Не выдавать TO-BE за AS-IS, INFERRED за CONFIRMED или один источник за истину при доказанном противоречии.

## AS-IS Evidence Loop

- **Goal:** достаточная модель текущего поведения для определения DELTA и рисков.
- **State:** проверенные утверждения, evidence, confidence, contradictions и unknowns.
- **Progress:** конкретное утверждение подтверждено, опровергнуто или честно ограничено.
- **Exit:** критичное AS-IS подтверждено; нерелевантные части не исследуются.
- **Stop:** новый проход не меняет модель или требует недоступного evidence.

## TO-BE Closure Loop

- **Goal:** однозначный и проверяемый целевой контракт.
- **State:** requirements, scenarios, examples, gaps и traceability.
- **Progress:** закрыт gap, устранено противоречие или добавлен проверяемый критерий.
- **Exit:** требования атомарны; сценарии покрывают риск; acceptance и verification связаны.
- **Stop:** gap принадлежит Рексу или владельцу.

## DELTA & Transition Safety Loop

- **Goal:** безопасный переход от подтверждённого AS-IS к TO-BE.
- **State:** DELTA, intermediate states, compatibility, migration, rollback и recovery.
- **Progress:** устранён или доказательно принят конкретный переходный риск.
- **Exit:** add/change/preserve/remove определены; инварианты и recovery защищены.
- **Stop:** требуется новое архитектурное решение → `SPEC GAP` Рексу.

Не повторять анализ другими словами. При циклически отменяющих друг друга правках остановиться и показать противоречие.
