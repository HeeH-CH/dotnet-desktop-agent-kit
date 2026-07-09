---
name: winui-app-edge-boundaries
description: Keeps WinUI 3 and Windows desktop platform authority at the App/View host edge during architecture, refactoring, audit, and build-fix work. Use when code touches Window, XamlRoot, AppWindow, HWND, dialogs, clipboard, file pickers, process launch, focus, tray, timers, WinUI controls, MSAL/WAM parent-window routing, or other desktop UI/platform boundaries.
---

# WinUI App Edge Boundaries

## Load first

Read these rule files when present:

- `../../rules/app-edge-boundaries.md`
- `../../rules/winui-codebehind.md`
- `../../rules/architecture-boundaries.md`

If a rule file is unavailable, apply this skill and the local project conventions.

## Boundary rule

Keep platform authority at the App/View host edge.

Allowed at the edge:

- `Window`, `XamlRoot`, `AppWindow`, `DispatcherQueue`, raw HWND, DWM/User32 interop
- dialogs, flyouts, focus, keyboard routing, pointer capture, tray, storyboard, timer
- clipboard, file picker, process launch, browser launch, local OS integration
- MSAL/WAM parent-window routing and interactive authentication surfaces

Do not move these authorities into ViewModels, Application services, Domain models, reducers, stores, or use cases.

## Refactoring workflow

1. Identify the platform authority being used.
2. Name the App-edge owner: View, Window, App service, presenter, adapter, or factory.
3. Replace inward references to WinUI/platform types with application-owned inputs, outputs, ports, or intents.
4. Keep ViewModels focused on commands, state, and use case calls.
5. Keep Application focused on orchestration and machine-readable results.
6. Keep Domain free of UI, platform, SDK, and OS concepts.

## Acceptable patterns

- View handles `XamlRoot` and passes a plain decision or request to the ViewModel.
- App-edge presenter maps an application result to a dialog, toast, flyout, or focus action.
- Infrastructure adapter uses a platform handle only behind an Application port when the handle cannot be avoided.
- Authentication composition keeps MSAL/WAM parent-window selection in App or a clearly named App-edge service.

## Anti-patterns

- Injecting `Window`, `XamlRoot`, `AppWindow`, HWND, or WinUI controls into a ViewModel.
- Passing UI controls through Application or Domain APIs.
- Making reducers or stores open dialogs, mutate controls, launch processes, or access clipboard/file pickers.
- Hiding platform calls behind generic service locators that can be resolved from any layer.

## Verification

Use targeted search and semantic checks when available:

- Search for WinUI/platform types in ViewModels, Application, Domain, reducers, stores, and use cases.
- Confirm App-edge APIs are owned by View, Window, App, presenter, adapter, or factory code.
- Confirm inward layers expose plain DTOs, intents, results, or ports instead of platform handles.
