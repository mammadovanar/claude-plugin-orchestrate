# Деливераблы Рекса

Выбирать один минимально достаточный формат или объединять совместимые секции без дублирования.

## Problem framing

- Raw request
- Real problem
- Problem owner
- Desired outcome
- Error cost
- Confirmed facts
- Assumptions / unknowns
- Hidden scenarios
- Guiding approach
- Next decision

## Requirements / architecture note

- Goal and context
- Roles and scenarios
- Business rules and invariants
- AS-IS / TO-BE
- System boundaries and affected contracts
- Data, state and lifecycle
- Failure, recovery and security consequences
- Open decisions
- Verification strategy

## Engineering task

- Goal
- Context / confirmed facts
- Scope
- Out of scope
- Implementation tasks
- Acceptance criteria
- Do not break
- Verification steps
- Definition of done
- Owner and next handoff

Формулировать задачи как результаты и контракты. Не предписывать реализацию там, где исполнитель должен сохранить инженерную свободу.

## Risk map

Для каждого существенного риска указать:

- событие и причина;
- затронутого владельца;
- вероятность / влияние;
- обнаружение;
- предотвращение или containment;
- recovery;
- остаточный риск.

## Agent handoff

```yaml
agent: Рекс
stage: framing
status: done | partial | blocked
shape: trivial | linear | parallel
goal: <наблюдаемый результат>
confirmed_facts:
  - <факт и evidence>
assumptions:
  - <явное допущение>
scope:
  - <входит>
out_of_scope:
  - <не входит>
do_not_break:
  - <инвариант>
acceptance_criteria:
  - <проверяемый критерий>
verification:
  - <проверка и ожидаемое доказательство>
open_questions:
  - <развилка владельцу или none>
next_owner: <роль>
next_action: <одно конкретное действие>
packages:
  - <только для действительно независимых частей>
```

## Финальная проверка

- Решается настоящая проблема, а не симптом.
- Владелец и цена ошибки определены.
- Критические утверждения подтверждены или помечены неизвестными.
- Скрытые сценарии и системные последствия раскрыты.
- Scope мал, но даёт реальный результат.
- Acceptance criteria наблюдаемы.
- Следующий владелец может продолжить без догадок.
