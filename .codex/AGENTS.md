# Codex CLI Agent Guide

Read the root `AGENTS.md` first. This file adds Codex CLI routing and execution preferences.

## Default Codex behavior

- Treat this repository as an agent skill kit, not as a runnable sample app.
- Prefer small, reviewable edits that keep Markdown structure consistent.
- Use Windows/PowerShell-compatible guidance for desktop projects unless the user explicitly asks otherwise.
- Do not require bash-only hooks as defaults.
- Keep public examples generic and free of secrets.
- When generating C# examples, use generic namespaces such as `ExampleApp.Application.Calendar`, `ExampleApp.Infrastructure.Graph`, and `ExampleApp.App.ViewModels`.
- Do not add product-specific tenant, workspace, account, organization, private URL, or customer details to shared rules, templates, skills, workflows, or agent instructions.

## Required reading order

1. `AGENTS.md`
2. This file
3. Task workflow under `workflows/`
4. Relevant agent file under `agents/`
5. Relevant skills under `skills/`
6. Relevant rules under `rules/`

## Routing table

| User asks for | Use workflow | Agent | Skills | Rules |
|---|---|---|---|---|
| new screen or feature | `workflows/add-feature.md` | `agents/dotnet-desktop-architect.md` | `skills/feature-planning/SKILL.md`, `skills/usecase-design/SKILL.md`, `skills/viewstate-design/SKILL.md` | `rules/architecture-boundaries.md`, `rules/mvi-state-flow.md` |
| code-behind cleanup | `workflows/migrate-code-behind.md` | `agents/mvvm-mvi-refactorer.md` | `skills/screen-refactoring/SKILL.md`, `skills/mvvm-mvi-refactoring/SKILL.md` | `rules/winui-codebehind.md`, `rules/viewmodel-responsibility.md` |
| ViewModel refactor | `workflows/refactor-screen.md` | `agents/mvvm-mvi-refactorer.md` | `skills/mvvm-mvi-refactoring/SKILL.md`, `skills/viewstate-design/SKILL.md` | `rules/mvi-state-flow.md`, `rules/usecase-boundaries.md` |
| Graph/M365 integration | `workflows/add-graph-integration.md` | `agents/graph-integration-specialist.md` | `skills/graph-adapter/SKILL.md`, `skills/usecase-design/SKILL.md` | `rules/infrastructure-adapters.md`, `rules/async-and-cancellation.md` |
| mid-refactor review | `workflows/mid-refactor-review.md` | `agents/quality-auditor.md` | `skills/roslyn-mcp-audit/SKILL.md`, `skills/verification/SKILL.md` | `rules/verification.md`, `rules/testing-strategy.md` |
| prepare a PR | `workflows/prepare-pr.md` | `agents/documentation-maintainer.md` | `skills/verification/SKILL.md`, `skills/codex-workflow/SKILL.md` | `rules/public-repo-safety.md`, `rules/naming-and-folder-conventions.md` |
| broad multi-area refactor | `workflows/parallel-wave.md` | `agents/quality-auditor.md` plus scoped specialists | `skills/roslyn-mcp-audit/SKILL.md`, `skills/verification/SKILL.md` | `rules/parallel-wave.md`, `rules/error-learning.md` |
| runtime smoke check | `workflows/runtime-smoke.md` | `agents/quality-auditor.md` | `skills/verification/SKILL.md` | `rules/app-edge-boundaries.md`, `rules/verification.md` |

## Platform default

For new Windows desktop guidance, assume WinUI 3 with Windows App SDK unless the target repository is WPF, the user explicitly asks for WPF, or the task is migration/comparison work. Do not remove WPF support from generic guidance.

## App-edge and results

Keep window, XAML, dialog, focus, clipboard, file picker, process launch, shell integration, native handle, and interactive auth authority at the App edge. Do not push raw WinUI/WPF types, `Window`, `XamlRoot`, HWND, or platform handles into ViewModels, Application, or Domain.

For user-visible operations, prefer typed result taxonomy over plain `bool`, raw `Exception`, or direct `exception.Message`. Results should expose action kind, status or severity, machine-readable failure reason, retry/reload/stale/cancelled/partial-success hints when relevant, and optional diagnostics references.

## Roslyn MCP first

When a Roslyn MCP server is available, use it before broad C# edits: project graph, references, implementations, diagnostics, cycles, dead code, public API surface, ViewModel SDK leakage, Application/Domain UI references, and DTO leakage to ViewState.

If Roslyn MCP is unavailable, say so in the final report and use `dotnet build`, `dotnet test`, and targeted text search as fallback.

Load the solution or relevant workspace before relying on Roslyn semantic answers. Roslyn supports analysis; it does not replace targeted build or test verification when behavior changes.

## PowerShell-friendly verification examples

```powershell
dotnet build
dotnet test
```

Do not make Linux-only shell pipelines mandatory in user projects.

## Completion report format

End Codex CLI tasks with Summary, Changed files, Architecture impact, Verification table, and Remaining risks.
