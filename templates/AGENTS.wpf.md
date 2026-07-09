# AGENTS.md for a WPF Desktop App

Use this file as the project-level agent guide for a WPF app.

## Architecture

```text
ExampleApp.App              WPF views, XAML, ViewModels, ViewState, commands
ExampleApp.Application      UseCases, ports, DTOs, Result models
ExampleApp.Domain           Pure domain concepts and rules
ExampleApp.Infrastructure   Graph, auth, files, local storage, external APIs
```

Dependency direction: `App -> Application -> Domain`, `Infrastructure -> Application / Domain`, `Domain -> no external dependencies`.

## WPF rules

- Code-behind is view-only.
- ViewModels expose ViewState and commands; they do not call SDKs directly.
- UseCases own application flow.
- Infrastructure owns adapters for Graph, auth, files, storage, and external APIs.
- Application and Domain must not reference `System.Windows` or WPF control types.

## Default flow

```text
View -> Command/Intent -> ViewModel -> UseCase -> Port -> Adapter -> Result -> ViewState -> View
```

## Verification

Run or report `dotnet build`, `dotnet test`, and Roslyn MCP project graph/reference/diagnostic checks when available.
