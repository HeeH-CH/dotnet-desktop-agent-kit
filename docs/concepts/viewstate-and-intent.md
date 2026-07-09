# ViewState and Intent

ViewState and Intent make desktop MVVM flows easier for agents to reason about.

## Intent

An intent is a user-visible action entering the ViewModel. It is commonly implemented as a command method, such as `LoadCalendarAsync`, `RefreshTasksAsync`, or `SelectItem`.

Intent methods should coordinate UI state and call UseCases. They should not perform SDK calls or application policy directly.

## ViewState

ViewState is the screen's bindable state. It should be explicit enough that the View can render without inferring hidden combinations.

```csharp
namespace ExampleApp.App.ViewModels;

public sealed record CalendarViewState(
    bool IsLoading,
    IReadOnlyList<CalendarEventItem> Events,
    string? ErrorMessage,
    bool IsEmpty);
```

## Result to ViewState

A UseCase returns an application-level Result. The ViewModel reduces that result into ViewState. External SDK DTOs, HTTP response objects, Infrastructure models, exceptions, secrets, and tenant-specific values must not enter ViewState.
