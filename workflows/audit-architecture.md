# Workflow: Audit Architecture

## Goal

Audit a desktop app for Clean Architecture, MVI-style state flow, and SDK leakage.

## When to use

Before a major refactor, after feature work, or when the user asks for an architectural health check.

## Inputs

- Solution/project path.
- Layer rules.
- Target feature/screen, if any.
- Known risks.

## Steps

1. Load `agents/quality-auditor.md` and `skills/roslyn-mcp-audit/SKILL.md`.
2. Inspect project graph and references.
3. Find Application/Domain references to UI frameworks.
4. Find ViewModel references to Infrastructure or Graph SDK.
5. Find port/interface implementations.
6. Check circular dependencies and diagnostics.
7. Check dead code and public API surface.
8. Check Infrastructure DTO leakage into ViewState.
9. Rank findings by severity and recommend fixes.

## Roslyn MCP checks

- Project graph.
- Symbol references.
- Port implementations.
- Circular dependencies.
- Diagnostics.
- Dead code.
- Public API surface.

## Expected file changes

- Audit report.
- Issue list.
- Suggested follow-up workflow.

## Verification

| Check | Result | Notes |
|---|---|---|
| Roslyn MCP | pass/fail/not available | semantic audit scope |
| Architecture boundaries | pass/fail | violations |
| Public API surface | pass/fail/not applicable | changes |

## Final report format

Audit table with severity, evidence, location, recommendation, status, and next workflow.
