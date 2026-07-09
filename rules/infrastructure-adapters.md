# Infrastructure Adapter Boundary

## Intent

Keep external systems replaceable and testable.

## Rule

External systems must be accessed through Application ports and Infrastructure adapters.

## External systems include

- Microsoft Graph
- Planner
- Calendar
- To Do
- authentication providers
- file system
- local cache
- databases
- HTTP APIs

## Preferred pattern

```text
Application Port
  ICalendarGateway
  IPlannerGateway
  IAuthTokenProvider

Infrastructure Adapter
  GraphCalendarGateway
  GraphPlannerGateway
  MsalAuthTokenProvider
```

## Violations

- ViewModel depends on `GraphServiceClient`.
- UseCase constructs SDK clients.
- Domain model contains external DTOs.
- ViewState exposes SDK response objects.

## Agent verification

Search for external SDK types outside Infrastructure. If found, propose a port and adapter extraction plan.
