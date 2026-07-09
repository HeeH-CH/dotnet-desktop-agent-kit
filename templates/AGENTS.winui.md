# AGENTS.md for a WinUI 3 Desktop App

Use this file as the project-level agent guide for a WinUI 3 app.

## Architecture

```text
ExampleApp.App              WinUI 3 views, XAML, ViewModels, ViewState, commands
ExampleApp.Application      UseCases, ports, DTOs, Result models
ExampleApp.Domain           Pure domain concepts and rules
ExampleApp.Infrastructure   Graph, auth, files, local storage, external APIs
```

Dependency direction: `App -> Application -> Domain`, `Infrastructure -> Application / Domain`, `Domain -> no external dependencies`.

## WinUI rules

- Code-behind is view-only.
- ViewModels use CommunityToolkit.Mvvm or equivalent MVVM patterns.
- ViewModel commands represent intents.
- UseCases perform application orchestration.
- Graph SDK, file IO, auth, and local storage implementations stay in Infrastructure.
- Application and Domain must not reference `Microsoft.UI.Xaml`.

## Default flow

```text
View -> Command/Intent -> ViewModel -> UseCase -> Port -> Adapter -> Result -> ViewState -> View
```

## Verification

Run or report `dotnet build`, `dotnet test`, and Roslyn MCP project graph/reference/diagnostic checks when available.
