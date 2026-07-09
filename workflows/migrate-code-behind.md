# Workflow: Migrate Code-Behind

## Goal

Move business/application logic out of WinUI/WPF code-behind into ViewModel intents and UseCases.

## When to use

A Page, Window, or UserControl event handler contains business logic, IO, or SDK calls.

## Inputs

- Code-behind file.
- Associated XAML and ViewModel.
- Desired behavior to preserve.

## Steps

1. Classify each handler as view-only, intent dispatch, or misplaced logic.
2. Move UI-only dispatch to commands/intents.
3. Move application branching/IO to UseCases.
4. Move SDK/file/auth details to Infrastructure adapters.
5. Update bindings/commands.
6. Keep focus/visual-tree-only logic in code-behind if needed.
7. Verify build and screen behavior.

## Roslyn MCP checks

- References from handler methods.
- Forbidden namespaces in code-behind.
- ViewModel command references.
- Diagnostics.

## Expected file changes

- Reduced code-behind.
- ViewModel intent methods.
- UseCases/ports/adapters if needed.
- Tests for moved behavior.

## Verification

| Check | Result | Notes |
|---|---|---|
| Code-behind business logic | pass/fail | remaining handlers |
| Build | pass/fail/not run | command |
| Bindings | pass/fail/not checked | affected names |

## Final report format

Moved logic summary, remaining view-only code, verification, and risks.
