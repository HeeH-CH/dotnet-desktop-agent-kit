# Codex Agent Configuration

This repository provides agent guidance for .NET desktop development.

Always read the root `AGENTS.md` first.

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

## Available rules

- `rules/architecture-boundaries.md`
- `rules/winui-codebehind.md`
- `rules/mvi-state-flow.md`
- `rules/infrastructure-adapters.md`
- `rules/verification.md`

## Tool preference

When a Roslyn MCP server is available, prefer semantic tools over broad file reads:

- project graph
- symbol search
- reference search
- implementation search
- diagnostics
- circular dependency detection
- dead code detection
