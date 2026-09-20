# Библиотека Зевса

Использовать один главный источник и максимум два вспомогательных. Не переносить в Зевса доменную или финансовую семантику: получать её из контрактов Рекса, Спеца, Афины или профильного владельца.

| Задача | Источник | Механизм |
| --- | --- | --- |
| Зрелый UI-паттерн | Tidwell, *Designing Interfaces* | Pattern fit по пользовательской задаче, данным и состояниям. |
| Visual polish | *Refactoring UI* | Hierarchy, spacing, sizing, contrast, grouping и emphasis. |
| Базовая композиция | Williams, *The Non-Designer's Design Book* | Contrast, repetition, alignment и proximity. |
| Понятность и feedback | Norman, *The Design of Everyday Things* | Signifiers, mapping, constraints, feedback и error prevention. |
| Быстрая очевидность | Krug, *Don't Make Me Think* | Удаление лишнего выбора и необходимости расшифровывать UI. |
| Формы | Wroblewski, *Web Form Design* | Field order, defaults, inline validation и error recovery. |
| Dashboard / данные | Few, *Information Dashboard Design* | Comparison, exception priority, density и drill-down. |
| Типографика | Lupton, *Thinking with Type* | Roles, scale, measure, rhythm и readability. |
| Сетка | Müller-Brockmann, *Grid Systems* | Grid, alignment, proportion и spatial order. |
| Цвет | Albers, *Interaction of Color* | Relative color, contrast и state distinction. |
| Бренд | Wheeler, *Designing Brand Identity* | Coherent expression, recognition, trust и consistency. |
| Platform behavior | Apple HIG / Material Design 3 | Native expectations, components и adaptive behavior. |
| Accessibility | WCAG 2.2 | Perceivable, operable, understandable, robust и измеримые checks. |
| Design system | Kholmatova, *Design Systems* | Tokens, variants, governance, reuse и change impact. |

## Recipe candidates

Если в среде доступна recipe-библиотека наподобие `ui-ux-pro-max`, использовать её только после определения visual intent.

1. Сформулировать нужный тип кандидата: style, color, typography, UX pattern или chart.
2. Получить 2–3 кандидата.
3. Проверить против Screen/Visual Contract, contrast, platform и существующих tokens.
4. Адаптировать, не копировать автоматически.
5. Если кандидат не улучшает решение, отказаться от него.

Рецепт даёт варианты; профессиональный контракт определяет решение.
