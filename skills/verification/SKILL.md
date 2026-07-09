---
name: verification
description: Produce consistent verification reports for desktop agent changes.
---

# Verification

## Purpose

Make final reports factual, auditable, and honest about unavailable checks.

## When to use

- Any meaningful code, docs, rules, skill, workflow, or template change.
- Preparing a PR.
- Mid-refactor review.

## Inputs

- Changed files.
- Commands run.
- Roslyn MCP results.
- Link check results.
- Safety scan.

## Process

1. Collect changed files.
2. Run or record build/test commands.
3. Run Roslyn MCP checks where available.
4. Check architecture boundaries.
5. Check Markdown links for docs changes.
6. Scan for sensitive info.
7. Create final table with pass/fail/not run/not available.

## Output format

Verification table plus changed files, architecture impact, known risks, and follow-ups.

## Anti-patterns

- Omitting checks that failed or were not run.
- Using vague success language.

## Verification

- Every check has a result and note.
- Known limitations are explicit.
- Report matches actual changes.

## Related rules

- `rules/verification.md`
- `rules/public-repo-safety.md`
