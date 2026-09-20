# UI implementation и verification

## Перед изменением

- Прочитать Screen Contract и do-not-distort.
- Исследовать существующий компонент, соседние экраны, tokens и локальный стиль.
- Определить минимальный scope и затронутых consumers.
- Отделить visual defect от UX/architecture gap.
- Сформулировать visual intent и verification plan.

## Реализация

- Переиспользовать tokens, primitives и components.
- Следовать локальной архитектуре и стилю кода.
- Делать минимальный reviewable diff.
- Реализовать затронутые loading, empty, error, disabled, focus, hover/pressed и success states.
- Обеспечить responsive/adaptive behavior без скрытого horizontal overflow.
- Сохранять semantic structure, keyboard/focus behavior и screen-reader contract.
- Не менять API, data model или бизнес-логику ради удобства UI.
- Не чинить несвязанные дефекты.

Если контракт невозможно выполнить существующими данными или API, вернуть gap вместо имитации поведения на клиенте.

## Engineering checks

Запустить применимые команды проекта: typecheck, lint, targeted tests, build и обязательные presubmit checks. Отделить pre-existing failure от регрессии своего изменения.

## Visual/runtime verification

Проверить по применимости:

- critical path и primary action;
- desktop/mobile и responsive breakpoints;
- loading, empty, error, disabled и success states;
- overflow, clipping, wrapping и content extremes;
- keyboard, focus и touch targets;
- contrast, readable type и zoom;
- state priority и опасные действия;
- отсутствие искажения бизнес-смысла.

Сделать screenshot или другое visual evidence, когда оно помогает review. Screenshot не заменяет прохождение interaction scenario.

## Exit

- Contract и do-not-distort соблюдены.
- Visual hierarchy однозначна.
- Решение согласовано с дизайн-системой.
- Затронутые viewport и states проверены.
- Accessibility checks выполнены.
- Engineering checks завершены.
- Runtime evidence приложено либо отсутствие проверки точно обозначено.
- Gaps переданы правильному владельцу.
