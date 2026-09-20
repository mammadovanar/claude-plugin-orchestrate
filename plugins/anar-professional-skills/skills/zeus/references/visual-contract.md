# Visual Contract и handoff

## Visual Contract

```yaml
screen_or_package: <название>
source_contract: <Афина / Screen Contract / local UI task>
visual_role: <что экран должен сообщить восприятием>
attention_order:
  first: <первое>
  second: <второе>
  third: <третье>
composition_density: <структура, ритм, плотность>
typography_roles:
  - <роль → treatment>
color_state_semantics:
  - <состояние → семантика>
patterns_components:
  - <выбор и причина>
brand_expression: <характер и доверие>
responsive_strategy: <mobile/desktop/adaptive>
accessibility:
  - <измеримое ограничение>
polish_risks:
  - <что сделает интерфейс слабым или недостоверным>
do_not_distort:
  - <UX/business/system invariant>
visual_freedom:
  - <что исполнитель может выбирать>
verification:
  - <scenario / viewport / state / evidence>
```

Не создавать полный контракт для Quick-задачи, если достаточно одного visual decision и проверки.

## Gap routing

```text
UX GAP: <неопределённый сценарий/IA/state> → <риск> → <что требуется от Афины>
ARCH GAP: <data/access/system problem> → <риск> → <что требуется от Рекса>
OWNER DECISION: <варианты> → <рекомендация> → <цена выбора>
```

## Handoff

```text
=== HANDOFF ===
AGENT: Зевс
STAGE: <visual-design | impl>
STATUS: <done | partial | blocked | needs-rework>
DESIGN SOURCE: <Athena handoff / Screen Contract / local UI task>
WORKTREE: <path | "-">
FILES TOUCHED: <files | "-">
VISUAL DECISIONS: <hierarchy, pattern, tokens, responsive/state treatment>
DO NOT BREAK: <UX, business and system invariants>
ENGINEERING CHECKS: <typecheck/lint/tests/build | not applicable>
VERIFY: <visual/runtime evidence | VISUAL VERIFY NOT RUN: ...>
GAPS: <UX GAP / ARCH GAP / owner decision | "-">
READY FOR: <independent review | afina:clarify | rex:reframe | owner:decision>
=== END HANDOFF ===
```
