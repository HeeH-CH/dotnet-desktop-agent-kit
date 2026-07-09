# Example: Calendar Feature Flow

This is a generic architecture example. It does not contain real tenant, client, redirect URI, organization, or account information.

## User intent

The user opens a Calendar screen and refreshes upcoming events.

## Flow

```text
CalendarView -> RefreshCalendarCommand -> CalendarViewModel.RefreshAsync -> LoadCalendarEventsUseCase -> ICalendarGateway -> GraphCalendarGateway -> LoadCalendarResult -> CalendarViewState -> CalendarView
```

## Application port

```csharp
namespace ExampleApp.Application.Calendar;

public interface ICalendarGateway
{
    Task<CalendarGatewayResult> GetUpcomingEventsAsync(DateRange range, CancellationToken cancellationToken);
}
```

## ViewModel stance

`CalendarViewModel` calls the UseCase and reduces `LoadCalendarResult` into `CalendarViewState`. It does not construct or call a Graph SDK client.
