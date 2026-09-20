# Деливераблы Афины

## UX Architecture Note

Для Deep-режима включать все применимые разделы; для Quick и Standard сокращать глубину, а не заполнять секции общими словами.

1. **Diagnosis** — проблема, владелец, риск, цель и метрика.
2. **Known / unknown** — evidence, assumptions и AMBIGUITY.
3. **Roles and scenarios** — вход, намерение, критический путь, решения, состояние выхода.
4. **Product structure / IA** — объекты, язык, группировка, иерархия и контексты.
5. **Screen map and navigation** — экраны, переходы и место в сценарии. Использовать Mermaid или таблицу, когда связь трудно объяснить линейно.
6. **State model** — loading, empty, error, partial, stale, restricted, success и recovery.
7. **Decision points** — что спрашивается, что система решает по умолчанию и почему.
8. **Screen Contracts** — только для ключевых экранов.
9. **System gaps** — backend, data, permission, migration или integration dependencies.
10. **Open decisions** — конкретный выбор владельцу с рекомендацией и ценой.
11. **Handoff** — задачи следующему владельцу и порядок.
12. **Verification** — scenario, state, error, accessibility, business и visual checks.

## Screen Contract

```yaml
screen: <название>
intent: <зачем существует>
role: <пользователь>
scenario_position: <до / здесь / после>
primary_action: <главное действие>
required_information:
  - <обязательное>
system_state:
  - <что должно быть видно>
risk: <какую ошибку или неопределённость снижает>
defaults:
  - <что решено системой и почему>
error_and_recovery:
  - <ошибка → восстановление>
emotional_outcome: <что человек должен чувствовать>
do_not_distort:
  - <инвариант для визуального слоя>
```

## Handoff визуальному дизайнеру

- UX diagnosis and target outcome
- Roles and critical scenarios
- Product structure and screen map
- Screen Contracts
- State priority
- Required and forbidden information
- Platform / accessibility constraints
- Business invariants
- Open visual freedom
- Verification required after design

Визуальному дизайнеру оставлять свободу формы внутри UX-контракта. Не предписывать декоративное решение.

## Verification

- **Scenario check** — достигается ли цель без скрытого тупика.
- **State check** — видны ли ключевые состояния и доверие к данным.
- **Error check** — предотвращаются ли ошибки и возможно ли recovery.
- **Accessibility check** — управление, фокус, размеры целей, контраст и текст.
- **Business check** — не нарушены ли деньги, роли, доступ, статусы и инварианты.
- **Feasibility check** — выражает ли система обещанное поведение.
- **Visual check** — после дизайна; если не выполнен, написать `VISUAL VERIFY NOT RUN: <причина> → <что проверить>`.
