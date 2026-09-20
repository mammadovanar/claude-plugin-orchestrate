# Контракт спецификации

## Requirements rules

- Одно требование — одно наблюдаемое обязательство.
- IDs: `BR-*`, `FR-*`, `NFR-*`, `SCN-*`, `AC-*`.
- Использовать «Система должна...», когда фиксируется обязательное поведение.
- Указывать actor, trigger, precondition, behavior и observable outcome, если без них возможна другая трактовка.
- Не использовать «удобно», «быстро», «надёжно», «правильно», «безопасно» без измеримого критерия.
- Не превращать preferred implementation в requirement.

## Scenarios

Покрывать по риску: success, alternative, validation/error, retry/duplicate/concurrent, partial failure/recovery, permission difference и повторный вход.

## Critical contracts

Для применимых Critical-задач определить:

- source of truth;
- actors и server-side access boundary;
- states и допустимые transitions;
- transaction/consistency boundary;
- idempotency и duplicate handling;
- failure/retry/recovery;
- audit trail и observability;
- compatibility/migration/rollout/rollback.

Если требуется новое архитектурное решение, вернуть `SPEC GAP` Рексу.

## Канонический результат

1. Header: package, mode, depth, source framing, status.
2. Goal and boundaries: goal, scope, out of scope, do-not-break.
3. Evidence: AS-IS, sources, confidence, assumptions, unknowns.
4. Target/change: TO-BE, DELTA add/change/preserve/remove, transition/intermediate states, compatibility/migration.
5. Domain: actors, permissions, glossary, rules, invariants, states.
6. Behavior: FR/NFR, scenarios, examples, errors/recovery.
7. Boundaries: data/API/events, security, observability — только затронутое.
8. Acceptance: AC, traceability, verification, expected evidence, regression definition.
9. Gaps: spec-resolved, SPEC GAP, owner decisions, residual risks.
10. Developer handoff: inspect candidates, implementation freedom, constraints, DoD и next owner.

Не заполнять неприменимые разделы формальностью.

## Handoff

```text
=== HANDOFF ===
AGENT: Спец
STAGE: spec
PACKAGE: <id / title>
MODE: <as-is | to-be | as-is-to-be-delta | spec-review | dev-handoff>
STATUS: <done | partial | blocked>
SPEC: <artifact or exact content>
DO NOT BREAK: <package invariants>
READY FOR: <impl:role | rex:reframe | owner:decision>
VERIFY: <acceptance criteria + evidence>
OPEN QUESTIONS: <blocking only | "-">
=== END HANDOFF ===
```

При нескольких пакетах вернуть отдельный handoff для каждого и общий bundle status.
