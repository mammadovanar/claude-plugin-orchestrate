---
name: orchestrate-code
description: Run a Google-style software engineering change process in Claude Code. Use directly for non-trivial code changes, risky changes, multi-agent work, production/data/security/payment/tenant/migration/API changes, or when the user asks for orchestration. The unit of work is a small reviewable change.
allowed-tools: Read, Grep, Glob, Bash, Edit, Write, Agent, TodoWrite
---

# Orchestrate Code

You are running an engineering change process, not just answering a coding request.

The unit of work is a **small reviewable change**:

```text
Change request -> framing -> sizing -> ownership -> implementation -> presubmit -> review -> integration -> release -> learning
```

## Execution Mode — Bypass (default for this user)

Run the whole process autonomously. Do NOT pause for human approval of the Change Plan and do NOT ask the user technical questions mid-flight.

- Produce the Change Plan, then proceed straight to implementation without waiting for sign-off.
- On uncertainty or a presubmit/review failure: route to `Ральф` for review → apply the fix → continue. Do not stop to ask the user.
- Use `AskUserQuestion` ONLY for genuine business decisions (product/UX trade-offs, money/policy choices, irreversible external actions), never for technical ones.
- Release is still gated by green presubmit/integration and an approved review — bypass removes human prompts, NOT the verification gates. Never mark unverified work as verified.
- This mirrors the user's standing "bypass mode" and "autonomous execution" mandate.

## Operating Rules

1. Change first, agent second.
2. Keep changes small, reviewable, and testable.
3. Separate author, reviewer, and release responsibilities.
4. Prefer Linear mode unless parallelism clearly pays for its coordination cost.
5. Presubmit before review.
6. Review before integration.
7. Integration before release.
8. Never describe unverified work as verified.
9. Preserve user changes and unrelated work.
10. Do not use parallel writers in one working tree.

## Agent Roster (this environment)

Delegate stages to existing subagents via the `Agent` tool, passing `subagent_type` = the agent's name. One agent must never be both author and independent reviewer of the same change.

| Stage / role                         | Agent (`subagent_type`) | Notes |
|--------------------------------------|-------------------------|-------|
| Framing / requirements / architecture| `Рекс`                  | Problem framing, risk map, engineering task. |
| Specification (AS-IS/TO-BE/DELTA)    | `Спец`                  | When a precise verifiable spec is needed before coding. |
| Author (non-trivial implementation)  | `Дима`                  | Senior practitioner; default author for hard changes. |
| Author (debug / regression / fast)   | `Денис`                 | Systematic debugging (Why Programs Fail). |
| Domain reviewer — finance/payments   | `Фил`                   | Money, P&L, posting, reconciliation. |
| Domain reviewer — UI/UX              | `Зевс`                  | Visual + UX correctness. |
| Reviewer (code/architecture/risk)    | `Ральф`                 | Independent review gate; never the author. |
| Release (commit/push/migrate/deploy) | `Гена`                  | Release ops ONLY. Project-agnostic: reads per-project access/config from the repo (e.g. `docs/deploy_access.md`, `DEPLOY_CHECKLIST.md`, `docs/runbooks/*`, `CONTRIBUTING.md`, `HANDOFF.md`). |

Rules for delegation:

- The author of a change must NOT be the agent that reviews it. If `Дима` authored, `Ральф` reviews. If `Денис` authored a fix, `Ральф` (or `Дима`) reviews.
- Release goes through `Гена` and nothing else touches commit/push/migrate/deploy.
- For trivial Express-mode changes you may author inline (no subagent) and skip review.
- A generic project may not have these agents; if a named agent is unavailable, fall back to authoring/reviewing inline and say so.

## Stage 0 - Intake

First restate briefly:

- what the user wants;
- what problem is actually being solved;
- risk class;
- reversibility;
- whether the change touches production, data, money, users, security, tenants, payments, migrations, external APIs, or release.

If the request is trivial and reversible, use Express mode.
If it is risky, multi-file, production-adjacent, or cross-domain, use Linear or Parallel mode.

## Stage 1 - Change Plan

Before coding, produce a Change Plan unless the task is clearly trivial.

Use this format:

```yaml
change_plan_schema: 1
request:
actual_problem:
risk: low|medium|high|critical
reversibility: easy|moderate|hard
recommended_mode: express|linear|parallel
why_this_mode:

changes:
  - change_id: CHG-001
    goal:
    owner:
    required_reviewers:
    likely_files:
    likely_contracts:
    data_impact:
    tenant_impact:
    security_impact:
    migration_impact:
    external_api_impact:
    presubmit_required:
    acceptance:
    rollback_note:

open_questions:
```

Bypass mode (this user): do not pause for Change Plan sign-off — record the plan and proceed to implementation. Reserve `AskUserQuestion` for business decisions only.

## Stage 2 - Mode Selection

### Express

Use when:

- one small reversible change;
- low blast radius;
- no production/data/money/security/tenant/payment/migration/release impact.

Flow:

```text
author -> minimal verification -> optional review -> done
```

### Linear

Default for non-trivial work.

Use when:

- changes depend on each other;
- fewer than three independent submit-ready changes exist;
- hidden dependencies are likely;
- domain risk is meaningful.

Flow:

```text
framing -> one author -> presubmit -> review -> integration -> release if needed
```

### Parallel

Use only when there are at least three independent, submit-ready changes.

Independent means:

- file sets do not overlap;
- contracts do not overlap;
- migrations do not overlap;
- generated files do not overlap;
- runtime flows do not depend on one another;
- each change can be reviewed and integrated independently.

Flow:

```text
framing -> authors in separate worktrees -> presubmit per change -> review barrier -> integrate one by one -> release
```

When unsure between Linear and Parallel, choose Linear.

For Parallel mode, isolate each author in its own git worktree (Agent tool `isolation: "worktree"`) so concurrent writers never share a working tree.

## Stage 3 - Ownership

Assign responsibilities:

- Framing owner: defines problem, scope, acceptance, risk.
- Author: writes code for exactly one change.
- Reviewer: checks correctness, risk, readability, tests, contracts, and integration safety.
- Domain reviewer: required for finance, security, UI, payments, tenant isolation, database migrations, or external API behavior.
- Release owner: commit/push/migrate/deploy/verify only.

One agent must not be both author and independent reviewer of the same change.
Map roles to the Agent Roster above.

## Stage 4 - Implementation

The author must:

- inspect existing code before editing;
- stay inside the approved change scope;
- avoid opportunistic refactors;
- avoid touching unrelated files;
- preserve user changes;
- update tests or explain why not;
- update docs if behavior, API, deployment, or operation changed;
- return the required handoff.

For parallel writers, use separate worktrees.

## Stage 5 - Presubmit

Before review, run the smallest meaningful verification set:

- format if relevant;
- lint if relevant;
- typecheck/build if relevant;
- unit tests for touched area;
- contract/API tests for endpoints and webhooks;
- migration dry-run for migrations;
- runtime/visual check for UI;
- security/tenant isolation check for auth, roles, permissions, data access.

If verification was not run:

```text
VERIFY NOT RUN: <reason>
```

Unverified high-risk changes cannot be marked ready for release.

## Stage 6 - Review

Reviewer checks:

- Does the implementation solve the stated change?
- Is the change small enough to review?
- Are touched files and contracts accurately reported?
- Are data, tenant, security, and external API impacts handled?
- Are tests adequate?
- Is rollback possible?
- Is documentation updated if behavior changed?

Reviewer should not rewrite the change. If code needs fixes, return `needs_rework`.

Review verdict:

```yaml
review_status: approved|needs_rework|blocked
must_fix:
should_fix:
residual_risk:
ready_for:
```

## Stage 7 - Integration

Integrate one approved change at a time.

After each integration:

- run build/typecheck or equivalent;
- run affected tests;
- stop on failure;
- return failed change to author or create a separate integration-fix change.

Do not silently fix integration breakage in the main tree.

## Stage 8 - Release

Release only when:

- all intended changes are integrated;
- review is approved;
- presubmit/integration checks are green;
- no temporary worktrees or branches from the plan remain;
- migration and env-var risks are understood;
- rollback note exists for risky changes.

Release owner must not add features or refactor during release.
Delegate release operations to `Гена`, who reads the current project's release access/config files from the repo (deploy access, checklist, runbooks). If those files are absent, release inline and state the path used.

## Stage 9 - Learning

Record a short lesson when:

- review found a serious issue;
- integration failed;
- production verification failed;
- rollback happened;
- the same mistake repeated.

Lesson format:

```yaml
date:
project:
trigger:
mistake_or_risk:
new_rule:
where_to_apply:
```

Append project-specific lessons to the repo's `lessons.md` when one exists.

## Required Implementation / Review Handoff

Every implementation or review result must end with:

```yaml
handoff_schema: 2
change_id:
agent:
stage: framing|implementation|review|integration|release
status: done|partial|blocked|needs_rework

change_description:
  why:
  what_changed:
  user_visible_behavior:
  risk:
  rollback:

ownership:
  author:
  required_reviewers:
  domain_reviewers:

impact:
  files_touched:
  contracts_changed:
  database_migrations:
  tenant_scope_impact:
  security_impact:
  external_api_impact:

presubmit:
  format:
  lint:
  typecheck:
  tests:
  runtime_or_visual:
  reason_if_not_run:

ready_for:
open_questions:
```

## Final Response

Keep the final answer short:

- what changed;
- verification status;
- remaining risks;
- next recommended step.
