# AGENTS.md Template for WinUI Projects

Use this template in a WinUI project.

## Architecture

This project uses WinUI + MVVM + MVI-style state flow + Clean Architecture.

```text
App -> Application -> Domain
Infrastructure -> Application / Domain
```

## Rules

- Keep code-behind view-only.
- Keep ViewModels focused on state and intent dispatch.
- Put workflows in Application UseCases.
- Put external integrations behind Application ports.
- Put Microsoft Graph and platform SDK implementations in Infrastructure.
- Keep Domain pure.

## Flow

```text
View -> Command/Intent -> ViewModel -> UseCase -> Port -> Adapter -> Result -> ViewState
```

## Verification

After changes, report build status, layer impact, ViewModel changes, UseCase changes, adapter changes, and risks.
