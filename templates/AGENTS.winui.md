# AGENTS.md Template for WinUI 3 Projects

Use this template as a project-level `AGENTS.md` for a WinUI 3 desktop app.

Keep the guidance generic to this project. Do not add tenant, workspace, customer, account, internal URL, or organization-specific details unless the repository already treats them as non-secret project configuration.

## Architecture

This project uses WinUI 3 with Windows App SDK, MVVM, MVI-style state flow, and Clean Architecture.

```text
ExampleApp.App              WinUI 3 views, XAML, ViewModels, ViewState, commands
ExampleApp.Application      UseCases, ports, DTOs, Result models
ExampleApp.Domain           Pure domain concepts and rules
ExampleApp.Infrastructure   Graph, auth, files, local storage, external APIs
```

Dependency direction:

```text
App -> Application -> Domain
Infrastructure -> Application / Domain
Domain -> no external dependencies
```

Domain stays pure. Application owns use cases, ports, DTOs, validation, orchestration, and application-owned result models. Infrastructure implements ports for external SDKs, file/network/storage/auth, and platform services. App/Presentation owns WinUI views, XAML, code-behind, ViewModels, ViewState, commands, intent dispatch, composition, and navigation.

WPF guidance applies only when this repository is WPF, when the task explicitly asks for WPF, or when comparing/migrating between WPF and WinUI.

## Rules

- Keep code-behind view-only.
- Keep ViewModels focused on state and intent dispatch.
- Put workflows in Application UseCases.
- Put external integrations behind Application ports.
- Put Microsoft Graph and platform SDK implementations in Infrastructure.
- Keep Domain pure.
- Do not reference WinUI types from Application or Domain.
- Do not call external SDKs directly from ViewModels.
- Do not put business rules in converters, code-behind, or XAML event handlers.
- Prefer constructor injection for ViewModels and use cases.
- Build the service provider once at app startup.

## Flow

```text
View -> Command/Intent -> ViewModel -> UseCase -> Port -> Adapter -> Result -> ViewState -> View
```

Reducers and stores, when used, stay pure. Reducers compute next state from current state plus intent/result. Stores dispatch and publish. Async I/O, HTTP, SDK calls, database work, file access, and WinUI control mutation happen in use cases, controllers, effects, adapters, or App-edge services, then return typed results or intents.

## App-edge authority

Keep these concerns at the App/View host boundary:

- `Window`, `XamlRoot`, `AppWindow`, `DispatcherQueue`, HWND, DWM/User32 interop, and native window placement.
- Dialogs, flyouts, focus, pointer capture, keyboard routing, tray integration, storyboard, timers, and visual tree mutation.
- Clipboard, file pickers, process launch, shell integration, and local OS integration.
- MSAL/WAM parent-window routing and interactive authentication surfaces.

ViewModels, Application, and Domain should depend on project-owned abstractions, presenters, coordinators, factories, or ports instead of raw platform types.

## Result taxonomy

User-visible operations should return typed results instead of plain `bool`, raw `Exception`, or direct `exception.Message`.

Prefer result models with:

- action kind
- status or severity
- machine-readable failure reason
- retry, reload, stale, cancelled, or partial-success classification when relevant
- optional diagnostics log reference
- optional user-message key or presentation hint

Infrastructure maps SDK, OS, network, auth, and storage failures into application-owned failure reasons. Presentation maps those reasons to user-facing text.

## Tool routing

Use available tools and skills in this order:

- WinUI 3, Windows App SDK, XAML, binding, theming, packaging, UI testing, WPF migration, and Fluent design: winui plugin skills.
- CommunityToolkit.Mvvm ViewModels, `[ObservableProperty]`, `[RelayCommand]`, validation, and command generation: `mvvm-toolkit`.
- CommunityToolkit.Mvvm dependency injection: `mvvm-toolkit-di`.
- CommunityToolkit.Mvvm messenger patterns: `mvvm-toolkit-messenger`.
- Microsoft concepts, Windows App SDK, MSAL, Microsoft Graph, .NET, SDK APIs, code samples, and compile errors: `microsoft-docs`, `microsoft-code-reference`, and the `microsoft-learn` MCP server.
- C# semantic analysis, symbol/reference navigation, diagnostics, generated partial ViewModel relationships, and safe refactoring impact checks: `roslyn` MCP.
- External library/API documentation, framework setup, migrations, package behavior, and code examples: Context7 MCP. Resolve the library ID first unless the user already provided it.

If a preferred tool is unavailable, state that briefly and fall back to official documentation, existing project patterns, and targeted `rg`.

## Broad-change workflow

For substantial, risky, or multi-area work:

1. Plan the full local flow and identify ownership bundles.
2. Run read-only discovery or audit in parallel only when ownership is disjoint.
3. Implement scoped batches by owner bundle.
4. Re-audit against the plan, changed files, and architecture rules.
5. Run the narrowest meaningful verification.
6. Fix blocking findings and re-audit narrowly.

For small, obvious changes, act directly and verify narrowly.

## Verification

After meaningful changes, report:

- verification performed
- changed files
- layer boundary impact
- App-edge authority impact
- ViewModel, ViewState, command, or intent changes
- UseCase, port, or adapter changes
- result taxonomy changes
- known risks and follow-up notes
