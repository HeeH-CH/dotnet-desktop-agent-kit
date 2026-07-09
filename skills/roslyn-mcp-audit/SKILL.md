---
name: roslyn-mcp-audit
description: Use Roslyn MCP to audit C# desktop architecture boundaries, symbol usage, and refactor safety.
---

# Roslyn MCP Audit

## Purpose

Prefer semantic evidence over broad text search for C# dependency, reference, and public API checks.

## When to use

- Before or after large refactors.
- Moving ViewModel, UseCase, port, or adapter code.
- Checking for SDK leakage.
- Final verification requires architecture confidence.

## Inputs

- Solution path or project set.
- Target symbols/namespaces.
- Expected layer rules.
- Changed files or planned changes.

## Process

1. Inspect project graph and dependency direction.
2. Find references for moved/renamed symbols.
3. Find implementations of ports/interfaces.
4. Check diagnostics and nullable warnings.
5. Detect circular dependencies.
6. Detect dead code or unused public members.
7. Inspect public API surface changes.
8. Check ViewModel -> Infrastructure/Graph, Application/Domain -> UI, and Infrastructure DTO -> ViewState leakage.

## Output format

Audit table with finding, evidence, severity, location, recommended fix, and verification status.

## Anti-patterns

- Claiming semantic audit when only grep was used.
- Making large edits before checking references.

## Verification

- Each finding has evidence.
- Unavailable Roslyn MCP is explicitly reported.
- Fallback checks are listed when MCP is unavailable.

## Related rules

- `rules/verification.md`
- `rules/architecture-boundaries.md`
