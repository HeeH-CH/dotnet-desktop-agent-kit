# MVI-style State Flow

## Intent

Make UI state transitions explicit while staying compatible with MVVM.

## Applies to

ViewModels, commands, ViewState, reducers, and screen flows.

## Rule

User actions enter the ViewModel as intents and leave as ViewState updates. Long operations represent idle, loading, success, empty, error, and cancellation states explicitly.

## Allowed

- Command methods named by intent.
- A ViewState record/class as the screen state source of truth.
- Reducer-style methods mapping Result to ViewState.

## Not allowed

- Scattered flags that allow invalid state combinations.
- Direct UI control mutation after UseCase completion.
- External SDK DTOs in ViewState.
- Async work with no loading/error/cancel state.

## Preferred pattern

Define `ScreenViewState` and update it from intent handlers and reducer methods.

## Anti-pattern

Each command toggles unrelated properties independently until invalid states become possible.

## Agent verification

- Check every user action has an intent path.
- Check loading/success/empty/error states exist.
- Check external DTOs are mapped before ViewState.
