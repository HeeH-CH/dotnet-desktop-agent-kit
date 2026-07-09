---
name: graph-adapter
description: Designs Microsoft Graph adapter boundaries for .NET desktop applications.
---

# Microsoft Graph Adapter Skill

## Purpose

Use this skill when adding or refactoring Microsoft Graph integration in a desktop app.

## Core rule

Microsoft Graph SDK belongs in Infrastructure. Application defines ports. ViewModels call UseCases.

```text
ViewModel -> UseCase -> ICalendarGateway -> GraphCalendarGateway -> Microsoft Graph SDK
```

## Common ports

```csharp
public interface ICalendarGateway
{
    Task<IReadOnlyList<CalendarEventDto>> GetEventsAsync(DateRange range, CancellationToken ct);
}

public interface IPlannerGateway
{
    Task<IReadOnlyList<PlannerTaskDto>> GetTasksAsync(CancellationToken ct);
}
```

## Error handling

Graph failures should be translated into application-level errors:

- permission denied
- token expired
- network unavailable
- throttled
- resource not found
- unknown external failure

Do not expose raw SDK exceptions to ViewModels.

## Mapping guidance

- Graph SDK model -> Infrastructure DTO or adapter result
- Infrastructure DTO -> Application DTO or domain-friendly model
- Application result -> ViewState

## Anti-patterns

- `GraphServiceClient` injected into a ViewModel.
- ViewState containing Graph SDK response types.
- UseCase catching raw SDK exceptions in many places.
- Authentication logic duplicated across adapters.
