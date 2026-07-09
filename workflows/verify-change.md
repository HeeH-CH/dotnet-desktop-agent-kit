# Workflow: Verify Change

## Goal

Produce a factual verification report for code, docs, or template changes.

## When to use

Before final response, before PR, or after a risky refactor.

## Inputs

- Changed files.
- Commands run.
- Available Roslyn MCP checks.
- Expected architecture rules.

## Steps

1. Collect changed files.
2. Run build/test when a code project exists.
3. Run Roslyn MCP checks when available.
4. Check Markdown links for docs changes.
5. Check rules/skills/agents/workflows naming consistency.
6. Scan for public-safety issues.
7. Write verification table.

## Roslyn MCP checks

- Project graph.
- Diagnostics.
- Symbol references.
- Forbidden dependency references.

## Expected file changes

- Verification report.
- Docs updates if verification exposes inconsistencies.

## Verification

| Check | Result | Notes |
|---|---|---|
| Markdown links | pass/fail | docs scope |
| README sync | pass/fail | EN/KO |
| Public safety | pass/fail | sensitive info scan |

## Final report format

Verification table, changed files, not-run reasons, and risks.
