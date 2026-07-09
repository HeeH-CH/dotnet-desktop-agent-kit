# MVI-style State Flow

## Intent

Make UI behavior explicit, predictable, and easier to refactor.

## Rule

Represent user actions as intents and screen output as ViewState.

```text
Intent -> UseCase -> Result -> Reducer / State update -> ViewState
```

## ViewState should include

- loading state
- empty state
- error state
- success/content state
- selected item state
- validation state when relevant

## Avoid

- scattered boolean flags with unclear combinations
- direct UI mutation after async work
- hidden state in services
- ViewModel methods that both call infrastructure and mutate many unrelated properties

## Preferred naming

- `LoadCalendarIntent`
- `CreateTaskIntent`
- `DashboardViewState`
- `CalendarPanelState`
- `Reduce(result)` or explicit state transition methods

## Agent verification

When changing a screen, list the possible states before modifying code. If a new async operation is added, define loading, success, and failure behavior.
