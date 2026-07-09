# Codex Agent Configuration

This repository provides agent guidance for .NET desktop development.

Always read the root `AGENTS.md` first.

Keep the kit generic. Do not add product-specific tenant, workspace, account, or organization details to shared rules, templates, skills, or agent instructions.

## Available specialist agents

| Agent | File | Use when |
|---|---|---|
| dotnet-desktop-architect | `agents/dotnet-desktop-architect.md` | Architecture decisions, layer boundaries, project references |
| mvvm-mvi-refactorer | `agents/mvvm-mvi-refactorer.md` | ViewModel cleanup, ViewState, Intent flow, code-behind removal |
| graph-integration-specialist | `agents/graph-integration-specialist.md` | Microsoft Graph, authentication, adapters, DTO mapping |
| quality-auditor | `agents/quality-auditor.md` | Architecture audits, Roslyn MCP analysis, dead code, cycles |
| build-fix-agent | `agents/build-fix-agent.md` | Build errors, nullable warnings, package/reference issues |

## Available skills

- `skills/architecture-advisor/SKILL.md`
- `skills/mvvm-mvi-refactoring/SKILL.md`
- `skills/clean-architecture-desktop/SKILL.md`
- `skills/graph-adapter/SKILL.md`
- `skills/winui-app-edge-boundaries/SKILL.md`
- `skills/mvi-reducer-store/SKILL.md`
- `skills/desktop-result-taxonomy/SKILL.md`
- `skills/desktop-composition-di/SKILL.md`

## Available rules

- `rules/architecture-boundaries.md`
- `rules/winui-codebehind.md`
- `rules/mvi-state-flow.md`
- `rules/infrastructure-adapters.md`
- `rules/verification.md`
- `rules/app-edge-boundaries.md`
- `rules/result-taxonomy.md`
- `rules/parallel-wave.md`
- `rules/error-learning.md`

## Available workflows

- `workflows/parallel-wave.md`
- `workflows/runtime-smoke.md`
- `workflows/verify-change.md`
- `workflows/refactor-screen.md`

Some rules, workflows, and skills may be added by separate upgrade bundles. When a listed path exists, read it before acting on that concern. When it does not exist, follow the root `AGENTS.md` operating guide and existing project patterns.

## Platform default

For new Windows desktop guidance, assume WinUI 3 with Windows App SDK unless the target repository is WPF, the user explicitly asks for WPF, or the task is migration/comparison work. Do not remove WPF support from generic guidance.

## App-edge and results

Keep window, XAML, dialog, focus, clipboard, file picker, process launch, shell integration, native handle, and interactive auth authority at the App edge. Do not push raw WinUI/WPF types, `Window`, `XamlRoot`, HWND, or platform handles into ViewModels, Application, or Domain.

For user-visible operations, prefer typed result taxonomy over plain `bool`, raw `Exception`, or direct `exception.Message`. Results should expose action kind, severity/status, machine-readable failure reason, retry/reload/stale/cancelled/partial-success hints when relevant, and optional diagnostics references.

## Tool and MCP routing

Use installed tools and skills in this order when available:

- WinUI 3, Windows App SDK, XAML, binding, theming, packaging, UI testing, WPF migration, and Fluent design: winui plugin skills.
- CommunityToolkit.Mvvm ViewModels, commands, validation, source generators: `mvvm-toolkit`.
- CommunityToolkit.Mvvm dependency injection: `mvvm-toolkit-di`.
- CommunityToolkit.Mvvm messaging: `mvvm-toolkit-messenger`.
- Microsoft concepts, tutorials, SDK APIs, code samples, compile errors, Windows App SDK, MSAL, Microsoft Graph, and .NET: `microsoft-docs`, `microsoft-code-reference`, and the `microsoft-learn` MCP server.
- C# semantic analysis, symbol/reference navigation, diagnostics, generated partial ViewModel relationships, and safe refactoring impact checks: `roslyn` MCP.
- External library/API documentation, framework setup, package behavior, migrations, and code examples: Context7 MCP. Resolve the library ID first unless already provided.

If the preferred tool is unavailable, say so briefly and fall back to official documentation, existing project patterns, and targeted `rg`.

## Tool preference

When a Roslyn MCP server is available, prefer semantic tools over broad file reads:

- project graph
- symbol search
- reference search
- implementation search
- diagnostics
- circular dependency detection
- dead code detection

Load the solution or relevant workspace before relying on Roslyn semantic answers. Roslyn supports analysis; it does not replace targeted build or test verification when behavior changes.
