---
name: desktop-composition-di
description: Designs and audits dependency injection composition for .NET desktop apps using constructor injection, a single startup service provider, explicit scopes/factories, and App-edge handling for WinUI, MSAL, window, and platform dependencies. Use when wiring services, ViewModels, windows, use cases, adapters, auth clients, or fixing DI/service locator issues.
---

# Desktop Composition and DI

## Load first

Read these rule files when present:

- `../../rules/architecture-boundaries.md`
- `../../rules/app-edge-boundaries.md`
- `../../rules/infrastructure-adapters.md`

If a rule file is unavailable, apply this skill and the local project conventions.

## Composition rule

Prefer constructor injection and one startup service provider.

Build the root provider once during application startup. Do not call `BuildServiceProvider()` from feature code, ViewModels, use cases, adapters, or repeated factory paths.

## Preferred shape

```text
App startup
  -> configure services
  -> build root provider once
  -> create Window/View/ViewModel through explicit factories or scopes
  -> dispose scopes/provider at the appropriate lifetime boundary
```

## Registration guidance

- Register ViewModels, use cases, ports, adapters, stores, reducers, and presenters with explicit lifetimes.
- Use constructor injection for dependencies.
- Use factories for runtime parameters, windows, dialogs, and monitor/window-scoped objects.
- Use scopes for window-specific or workflow-specific lifetimes.
- Keep Application and Domain independent from Infrastructure and App registrations.

## App-edge dependencies

Keep WinUI/MSAL parent-window authority in App or an App-edge service:

- `Window`, `XamlRoot`, `AppWindow`, HWND, and WinUI controls stay outside ViewModels and Application.
- MSAL/WAM parent-window routing stays in App composition or an App-edge auth presenter/factory.
- Use plain ports or request objects inward when Application needs an auth-capable workflow.
- Do not pass parent window handles through Domain or general Application services.

## Service locator limits

Avoid service locator access from arbitrary code. If compatibility requires it:

- isolate it behind a named composition facade
- keep usage at App edge or migration boundaries
- do not use it to hide missing constructor dependencies
- plan a path to explicit constructors or factories

## Audit checklist

- There is only one root provider build in startup.
- Constructor dependencies reveal the actual collaboration graph.
- Feature code does not create nested root providers.
- ViewModels do not resolve services ad hoc.
- Window-scoped services have explicit factories or scopes.
- App-edge platform dependencies are not injected into Application or Domain.
