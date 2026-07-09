# Workflow: Mid-refactor Review

## Goal

Pause during a refactor to assess buildability, boundary direction, and remaining risk.

## When to use

A refactor is partly complete, risky, or has accumulated uncertainty.

## Inputs

- Current branch/diff.
- Target workflow.
- Known failures.
- Remaining goals.

## Steps

1. List changed files and classify by layer.
2. Run or review build/test diagnostics.
3. Run Roslyn MCP checks when available.
4. Find partially migrated responsibilities.
5. Check whether bindings or public contracts changed.
6. Identify smallest next safe step.
7. Recommend stop, continue, or rollback decision.

## Roslyn MCP checks

- Diagnostics.
- Symbol references.
- Forbidden dependency references.
- Dead code.

## Expected file changes

- Review report.
- Next-step plan.
- Risk list.
- Rollback notes if needed.

## Verification

| Check | Result | Notes |
|---|---|---|
| Build | pass/fail/not run | current state |
| Boundary direction | pass/fail | partial violations |
| Next step | ready/blocked | reason |

## Final report format

State summary, findings, next safe step, risks, and rollback notes.
