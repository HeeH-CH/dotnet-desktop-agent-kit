# Workflow: Prepare PR

## Goal

Prepare a branch for review with documentation, verification, and public-safety checks.

## When to use

Before opening a PR or asking for final review.

## Inputs

- Branch name.
- Changed files.
- Verification results.
- Issue or task context.

## Steps

1. Check branch diff against base.
2. Run Markdown link checks for docs.
3. Run build/test if code exists.
4. Run Roslyn MCP audit if C# changes exist.
5. Check public-safety rules.
6. Update README/AGENTS/docs consistency.
7. Write PR summary and verification table.
8. Open PR if tool access allows.

## Roslyn MCP checks

- Diagnostics for code changes.
- References for moved symbols.
- Project graph for dependency changes.

## Expected file changes

- PR description.
- Updated docs if gaps are found.
- Final verification report.

## Verification

| Check | Result | Notes |
|---|---|---|
| git status / branch diff | pass/fail | changed files |
| Markdown links | pass/fail | relative links |
| Public safety | pass/fail | sensitive info scan |

## Final report format

Summary, major additions, architecture intent, sensitive information check, verification, commits, and PR link.
