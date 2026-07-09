# Codex CLI Agent Guide

Read the root `AGENTS.md` first. This file adds Codex CLI routing and execution preferences.

## Default Codex behavior

- Treat this repository as an agent skill kit, not as a runnable sample app.
- Prefer small, reviewable edits that keep Markdown structure consistent.
- Use Windows/PowerShell-compatible guidance for desktop projects unless the user explicitly asks otherwise.
- Do not require bash-only hooks as defaults.
- Keep public examples generic and free of secrets.
- When generating C# examples, use generic namespaces such as `ExampleApp.Application.Calendar`, `ExampleApp.Infrastructure.Graph`, and `ExampleApp.App.ViewModels`.

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

## Roslyn MCP first

When a Roslyn MCP server is available, use it before broad C# edits: project graph, references, implementations, diagnostics, cycles, dead code, public API surface, ViewModel SDK leakage, Application/Domain UI references, and DTO leakage to ViewState.

If Roslyn MCP is unavailable, say so in the final report and use `dotnet build`, `dotnet test`, and targeted text search as fallback.

## PowerShell-friendly verification examples

```powershell
dotnet build
dotnet test
```

Do not make Linux-only shell pipelines mandatory in user projects.

## Completion report format

End Codex CLI tasks with Summary, Changed files, Architecture impact, Verification table, and Remaining risks.
