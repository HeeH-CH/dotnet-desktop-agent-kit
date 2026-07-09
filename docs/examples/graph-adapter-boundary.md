# Example: Graph Adapter Boundary

This example is generic and intentionally omits real tenant IDs, client IDs, redirect URIs, organization names, and account details.

## Boundary

```text
Application port:        ICalendarGateway
Infrastructure adapter:  GraphCalendarGateway
External SDK:            Graph SDK types stay inside Infrastructure
Presentation state:      CalendarViewState with app-safe data only
```

## Application port

```csharp
namespace ExampleApp.Application.Calendar;

public interface ICalendarGateway
{
    Task<CalendarGatewayResult> GetUpcomingEventsAsync(DateRange range, CancellationToken cancellationToken);
}

public abstract record CalendarGatewayResult
{
    public sealed record Success(IReadOnlyList<CalendarEventDto> Events) : CalendarGatewayResult;
    public sealed record Throttled(TimeSpan? RetryAfter) : CalendarGatewayResult;
    public sealed record PermissionDenied : CalendarGatewayResult;
    public sealed record TokenExpired : CalendarGatewayResult;
    public sealed record NetworkUnavailable : CalendarGatewayResult;
    public sealed record UnknownExternalFailure(string Message) : CalendarGatewayResult;
}
```

## Infrastructure adapter stance

```csharp
namespace ExampleApp.Infrastructure.Graph;

using ExampleApp.Application.Calendar;

public sealed class GraphCalendarGateway : ICalendarGateway
{
    public Task<CalendarGatewayResult> GetUpcomingEventsAsync(DateRange range, CancellationToken cancellationToken)
    {
        // Real implementation calls the Graph SDK here, maps SDK DTOs to app DTOs,
        // and maps SDK exceptions to CalendarGatewayResult cases.
        throw new NotImplementedException();
    }
}
```

Raw SDK DTOs and exceptions must not cross into Application, ViewModel, or ViewState.
