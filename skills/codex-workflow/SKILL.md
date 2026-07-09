---
name: codex-workflow
description: Run this kit through Codex CLI with desktop-first routing, Windows-friendly commands, and clear final reports.
---

# Codex Workflow

## Purpose

Help Codex choose the right agent, skill, rule, workflow, and final report shape.

## When to use

- Using Codex CLI in a desktop app or this kit.
- User asks to commit, prepare PR, or perform multi-file docs changes.

## Inputs

- User task.
- Target repo and branch policy.
- Changed files.
- Available tools.

## Process

1. Read root AGENTS and `.codex/AGENTS.md`.
2. Pick workflow first, then agent, skills, and rules.
3. Prefer Roslyn MCP when available.
4. Use PowerShell/cross-platform commands unless repo is clearly Unix-only.
5. Make coherent commits.
6. Prepare final report with verification.

## Output format

Codex execution plan, selected files, verification, commit/PR summary.

## Anti-patterns

- Ignoring root AGENTS.
- Assuming bash hooks in Windows desktop projects.
- Reporting background work instead of current results.

## Verification

- Final report names workflow, checks, commit/PR status, and risks.

## Related rules

- `rules/verification.md`
- `rules/public-repo-safety.md`
