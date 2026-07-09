# dotnet-desktop-agent-kit

[한국어 README](README.ko.md)

A practical agent execution kit for building and refactoring .NET desktop applications with WinUI/WPF, MVVM, MVI-style state flow, Clean Architecture, and Roslyn MCP-assisted code analysis.

This project helps AI coding agents make safer architectural decisions and carry changes through planning, scoped implementation, audit, and verification when working on C# desktop applications.

## Focus

- Separate WinUI/WPF views from business logic.
- Keep ViewModels clean, state-driven, and testable.
- Use Intent -> UseCase -> Result -> ViewState flows.
- Enforce Clean Architecture boundaries in desktop applications.
- Isolate Microsoft Graph, file system, authentication, local storage, and external APIs behind adapters.
- Use Roslyn MCP tools for semantic code navigation, dependency analysis, dead-code detection, and refactoring audits.
- Route work across Codex, Claude, reusable rules, skills, workflows, specialist agents, and MCP tools at a high level.

## Why this exists

Most .NET agent kits and Clean Architecture examples are optimized for ASP.NET Core, Minimal APIs, EF Core, and backend systems. Desktop applications have different pressure points:

- XAML and code-behind can quietly accumulate application logic.
- ViewModels can become service containers.
- UI state often becomes scattered across mutable flags.
- External SDKs can leak directly into presentation code.
- Refactoring needs to preserve buildability and UI behavior step by step.

This kit exists to give AI coding agents explicit guidance for those desktop-specific problems. It is meant to be used as a practical execution kit, not only as a project scaffold.

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

## Execution surfaces

Use the kit as a set of coordinated surfaces:

- `AGENTS.md` and `.codex/AGENTS.md` define operating rules for Codex and other coding agents.
- `CLAUDE.md` gives Claude Code a lightweight entrypoint into the same guidance.
- `rules/` contains always-on architectural constraints for desktop code.
- `workflows/` contains repeatable procedures for refactoring, verification, and runtime checks.
- `skills/` contains callable task guides for common desktop architecture work.
- `agents/` defines specialist agents for architecture, refactoring, quality audit, and build fixes.
- MCP/tool routing tells agents when to prefer Roslyn MCP, Microsoft Learn/docs tools, Context7, WinUI plugin skills, and CommunityToolkit.Mvvm skills.

## Upgrade surface

The current upgrade turns the repository into a more complete execution kit. The planned and documented surfaces include:

- Rules: `rules/app-edge-boundaries.md`, `rules/result-taxonomy.md`, `rules/parallel-wave.md`, and `rules/error-learning.md`.
- Workflows: `workflows/parallel-wave.md`, `workflows/runtime-smoke.md`, `workflows/verify-change.md`, and `workflows/refactor-screen.md`.
- Skills: `skills/winui-app-edge-boundaries/`, `skills/mvi-reducer-store/`, `skills/desktop-result-taxonomy/`, and `skills/desktop-composition-di/`.
- Specialist agents: `agents/dotnet-desktop-architect.md`, `agents/mvvm-mvi-refactorer.md`, `agents/quality-auditor.md`, and `agents/build-fix-agent.md`.

These surfaces should stay generic. Do not add product-specific tenant, workspace, internal URL, secret, or customer details.

## How to use

Copy the pieces that match your AI coding tool and project:

- Use `AGENTS.md` as the main project-level agent guide.
- Use `.codex/AGENTS.md` for Codex CLI.
- Use `CLAUDE.md` for Claude Code.
- Import selected files from `rules/`, `skills/`, `agents/`, and `workflows/` into your project.
- Customize the examples to your real project structure.
- For broad refactoring, start from the relevant workflow, load the related rules and skills, delegate to specialist agents only where useful, then verify with the narrowest meaningful checks.

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

This is an early v0.1 execution kit. The current goal is to make desktop-agent work repeatable across rules, workflows, skills, specialist agents, and MCP/tool routing. Contributions are welcome, especially around:

- WinUI 3 patterns
- WPF patterns
- CommunityToolkit.Mvvm usage
- MVI-style desktop state handling
- Clean Architecture for desktop apps
- Roslyn MCP workflows
- Microsoft Graph adapter boundaries

## License

MIT
