# Workflow: Add Feature

## Goal

Add a WinUI/WPF desktop feature without leaking business logic or external SDKs into Presentation.

## When to use

A new screen, command, integration-backed feature, or user-visible workflow is requested.

## Inputs

- Feature name and target screen.
- Target framework: WinUI 3 or WPF.
- External data needs.
- Acceptance criteria.

## Steps

1. Read `AGENTS.md` and `.codex/AGENTS.md` when using Codex.
2. Load `agents/dotnet-desktop-architect.md`.
3. Define user intents and ViewState states.
4. Decide if a UseCase is needed.
5. Define Application DTOs and ports before Infrastructure.
6. Implement or document Infrastructure adapter boundaries.
7. Wire ViewModel command/intent to UseCase.
8. Update View bindings.
9. Verify build, tests, boundaries, and public safety.

## Roslyn MCP checks

- Project graph before/after.
- References from ViewModel to UseCase only.
- Port implementations in Infrastructure.
- Diagnostics and cycles.

## Expected file changes

- View/ViewModel/ViewState updates.
- Application UseCase/port/DTO additions.
- Infrastructure adapter addition if external IO is needed.
- Tests and docs when applicable.

## Verification

| Check | Result | Notes |
|---|---|---|
| Build | pass/fail/not run | command and important output |
| Tests | pass/fail/not run | scope |
| Roslyn MCP | pass/fail/not available | checks performed |
| Architecture boundaries | pass/fail | violations or none |
| Public safety | pass/fail | generic examples only |

## Final report format

Summary, changed files, architecture impact, verification table, risks, and follow-ups.
