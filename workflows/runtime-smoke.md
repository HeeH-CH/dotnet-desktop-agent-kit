# Workflow: Runtime Smoke

Use this for manual or interactive confidence after a desktop app change. This is not a replacement for build, tests, or automated UI checks.

## Intent

Confirm that the changed path can be exercised in a real app session without obvious runtime, windowing, binding, or presentation failures.

## Before running

1. Identify the exact user-visible path to exercise.
2. Identify required accounts, files, network access, feature flags, or test data.
3. Confirm whether app launch, interactive auth, browser, file picker, or external process use is allowed.
4. Keep the smoke path narrow and tied to the change.

## Smoke checks

- app starts or target window opens
- changed command or intent can be triggered
- loading, success, empty, cancellation, and failure states present correctly when practical
- dialogs, pickers, clipboard, process launch, and auth surfaces have correct parent-window behavior
- no obvious binding errors, crashes, hangs, or focus traps
- result messages are user-safe and do not expose raw `exception.Message`

## App-edge checks

For WinUI and Windows App SDK changes, confirm `Window`, `XamlRoot`, `AppWindow`, HWND, dialogs, timers, clipboard, file/process launch, and parent-window auth remain at the App/View host boundary or an explicit App-edge service.

## Report

```markdown
## Runtime Smoke Report

- Path exercised:
- Environment:
- Result:
- App-edge observations:
- Issues found:
- Not exercised:
```
