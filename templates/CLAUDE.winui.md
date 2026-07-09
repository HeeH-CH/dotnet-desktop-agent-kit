# CLAUDE.md for a WinUI 3 Desktop App

Read `AGENTS.md` first.

## Claude Code defaults

- Treat WinUI code-behind as view-only.
- Keep ViewModels focused on intents and ViewState.
- Move orchestration into Application UseCases.
- Keep Graph/M365 SDK usage in Infrastructure adapters.
- Prefer Roslyn MCP semantic analysis when available.
- Use generic examples and never add secrets.

## Suggested prompt

```text
Read AGENTS.md. Use the add-feature workflow.
Add the requested WinUI screen using MVVM + MVI-style state flow.
Keep external integrations behind Application ports and Infrastructure adapters.
Report build, tests, Roslyn MCP checks, and boundary impact.
```
