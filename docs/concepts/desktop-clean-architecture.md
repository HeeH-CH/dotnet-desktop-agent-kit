# Desktop Clean Architecture

Desktop Clean Architecture keeps WinUI/WPF UI concerns separate from application workflows, business concepts, and external adapters.

## Layers

```text
App / Presentation
  Views, XAML, ViewModels, ViewState, Commands, navigation, UI composition
Application
  UseCases, ports, DTOs, orchestration, validation, Result models
Domain
  Pure business concepts, value objects, domain rules, framework-independent models
Infrastructure
  Microsoft Graph, auth, local storage, file access, external APIs, adapter implementations
```

## Dependency direction

```text
App -> Application -> Domain
Infrastructure -> Application / Domain
Domain -> no external dependencies
```

The App project may be the composition root and wire dependencies. That does not mean ViewModels should directly use Infrastructure implementations.

## Practical boundary test

1. Would this code still make sense without WinUI/WPF? If yes, it may belong outside Presentation.
2. Would this code still make sense without Microsoft Graph or file IO? If yes, hide those details behind a port.
3. Is this a pure business rule? Put it in Domain.
4. Is this orchestration for a user action? Put it in Application.
5. Is this visual behavior only? Keep it in Presentation.

## Common desktop violations

- `GraphServiceClient` injected into a ViewModel.
- `Microsoft.UI.Xaml` referenced by Application.
- `System.Windows` referenced by Domain.
- External SDK DTO returned from a UseCase to the UI.
- Code-behind event handler performing authentication or file parsing.
