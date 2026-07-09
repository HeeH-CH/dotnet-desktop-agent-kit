# dotnet-desktop-agent-kit

A practical agent skill kit for building and refactoring .NET desktop applications with WinUI/WPF, MVVM, MVI-style state flow, Clean Architecture, and Roslyn MCP-assisted code analysis.

This project helps AI coding agents make safer architectural decisions when working on C# desktop applications.

## Focus

- Separate WinUI/WPF views from business logic.
- Keep ViewModels clean, state-driven, and testable.
- Use Intent -> UseCase -> Result -> ViewState flows.
- Enforce Clean Architecture boundaries in desktop applications.
- Isolate Microsoft Graph, file system, authentication, local storage, and external APIs behind adapters.
- Use Roslyn MCP tools for semantic code navigation, dependency analysis, dead-code detection, and refactoring audits.

## Why this exists

Most .NET agent kits and Clean Architecture examples are optimized for ASP.NET Core, Minimal APIs, EF Core, and backend systems. Desktop applications have different pressure points:

- XAML and code-behind can quietly accumulate application logic.
- ViewModels can become service containers.
- UI state often becomes scattered across mutable flags.
- External SDKs can leak directly into presentation code.
- Refactoring needs to preserve buildability and UI behavior step by step.

This kit exists to give AI coding agents explicit guidance for those desktop-specific problems.

## Recommended application architecture

```text
App / Presentation
  WinUI/WPF Views, XAML, ViewModels, ViewState, Commands, Intent dispatching

Application
  UseCases, Ports, DTOs, orchestration, validation, application-level Result models

Domain
  Pure business concepts, value objects, domain rules, framework-independent models

Infrastructure
  Microsoft Graph, authentication, local storage, file access, external APIs, adapter implementations
```

Dependency direction must remain inward:

```text
App -> Application -> Domain
Infrastructure -> Application / Domain
Domain -> no external dependencies
```

## MVI-style desktop flow

```text
View
 -> Command / Intent
 -> ViewModel
 -> UseCase
 -> Port
 -> Infrastructure Adapter
 -> Result
 -> Reducer / State update
 -> ViewState
 -> View
```

## Repository structure

```text
AGENTS.md                     # Main agent operating guide
CLAUDE.md                     # Optional Claude Code entrypoint
.codex/AGENTS.md              # Codex CLI-friendly entrypoint
rules/                        # Always-on architectural rules
skills/                       # Reusable task skills
agents/                       # Specialist subagent definitions
workflows/                    # Step-by-step development workflows
templates/                    # Copyable project templates
docs/adr/                     # Architecture decision records
```

## How to use

Copy the pieces that match your AI coding tool and project:

- Use `AGENTS.md` as the main project-level agent guide.
- Use `.codex/AGENTS.md` for Codex CLI.
- Use `CLAUDE.md` for Claude Code.
- Import selected files from `rules/`, `skills/`, `agents/`, and `workflows/` into your project.
- Customize the examples to your real project structure.

## Roslyn MCP recommendation

For C# projects, prefer semantic analysis over blind text search where possible. Useful Roslyn MCP operations include:

- find symbols and references
- find implementations of ports/interfaces
- inspect project dependency graph
- detect circular dependencies
- inspect diagnostics
- detect dead code
- inspect public API surface

## Status

This is an early v0.1 scaffold. The current goal is to establish the structure and vocabulary. Contributions are welcome, especially around:

- WinUI 3 patterns
- WPF patterns
- CommunityToolkit.Mvvm usage
- MVI-style desktop state handling
- Clean Architecture for desktop apps
- Roslyn MCP workflows
- Microsoft Graph adapter boundaries

## License

MIT
