# Workflow: Refactor Screen

## Goal

Refactor a screen toward MVVM + MVI-style state flow in small safe steps.

## When to use

A ViewModel or code-behind file is too large, state is scattered, or bindings are fragile.

## Inputs

- Target screen files.
- Known broken behavior or desired outcome.
- Build/test status.

## Steps

1. Snapshot code-behind, bindings, commands, properties, and injected services.
2. Load `agents/mvvm-mvi-refactorer.md`.
3. Identify business/application logic and external calls.
4. Extract UseCases for application logic.
5. Extract ports/adapters for external systems.
6. Create or normalize ViewState.
7. Preserve or deliberately update bindings.
8. Build/test after each meaningful slice.
9. Document remaining debt.

## Roslyn MCP checks

- Find references to ViewModel properties and commands.
- Check forbidden namespaces in ViewModel/code-behind.
- Check diagnostics after each slice.

## Expected file changes

- Code-behind reduction.
- ViewModel intent/state changes.
- UseCase/port/adapters if needed.
- Tests for state transitions.

## Verification

| Check | Result | Notes |
|---|---|---|
| Build | pass/fail/not run | command |
| Tests | pass/fail/not run | scope |
| Roslyn MCP | pass/fail/not available | checks |
| ViewState/Intent flow | pass/fail | screen impact |

## Final report format

Summary, before/after responsibilities, changed files, verification, and remaining risk.
