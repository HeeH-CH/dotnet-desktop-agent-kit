# CLAUDE.md

Use `AGENTS.md` as the primary operating guide. This file exists so Claude Code users can find the same desktop-first rules used by Codex CLI.

## Working stance

- Treat this repository as a public agent skill kit, not a runnable sample app.
- Keep guidance desktop-first: WinUI, WPF, MVVM, MVI-style state flow, Clean Architecture, Roslyn MCP.
- Do not import backend-only ASP.NET Core assumptions unless clearly marked as out of scope or optional.
- Keep all examples generic and public-safe.
- When changing one concept, update the corresponding rule, skill, agent, workflow, and docs when applicable.

## Load order

1. `AGENTS.md`
2. Relevant `rules/*.md`
3. Relevant `skills/*/SKILL.md`
4. Relevant `agents/*.md`
5. Relevant `workflows/*.md`

## Common tasks

- Feature planning: `workflows/add-feature.md`
- Screen refactoring: `workflows/refactor-screen.md`
- Graph integration: `workflows/add-graph-integration.md`
- Architecture audit: `workflows/audit-architecture.md`
- PR preparation: `workflows/prepare-pr.md`
