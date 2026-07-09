# App-edge Boundary Rule

## Intent

Keep desktop platform authority at the App/View host boundary so application logic remains testable, portable, and safe to refactor.

## Rule

WinUI, WPF, and native Windows authority belongs in the App, Window, Page, View host, or an explicit App-edge service. ViewModels, Application services, reducers, stores, and Domain models must not own raw platform handles or view-host authority.

## App-edge authority includes

- `Window`, `XamlRoot`, `AppWindow`, `DispatcherQueue`, and raw HWND values
- DWM, User32, shell, tray, focus, pointer capture, and keyboard routing interop
- dialogs, flyouts, popups, teaching tips, and parent-window routing
- UI timers, storyboards, animations, visual tree traversal, and control mutation
- clipboard, file picker, folder picker, save picker, process launch, and local OS integration
- interactive authentication surfaces that require a parent window

## Preferred pattern

```text
View / App host -> App-edge service -> UseCase / ViewModel
UseCase / ViewModel -> request model / result -> App-edge presenter
```

Pass stable request and result models inward. Keep `Window`, `XamlRoot`, `AppWindow`, HWND, controls, and platform event args at the boundary.

## Violations

- ViewModel stores `Window`, `XamlRoot`, `AppWindow`, HWND, or WinUI controls.
- Application or Domain service calls file pickers, dialogs, clipboard, process launch, or UI timers directly.
- Reducer or store mutates a control, opens a dialog, or schedules UI work.
- Authentication, dialog, or picker code loses parent-window ownership by running from a headless service.

## Agent verification

Search for App-edge types outside the App/View host layer. If a feature needs platform authority, introduce an explicit boundary service or presenter rather than moving raw UI authority inward.
