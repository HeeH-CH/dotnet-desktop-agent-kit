# Infrastructure Adapters

## Intent

Keep external systems replaceable and prevent SDK details from leaking into Presentation or Domain.

## Applies to

Microsoft Graph, auth, file access, local storage, external APIs, OS services.

## Rule

Application defines ports; Infrastructure implements them. Infrastructure maps external DTOs and exceptions to application-level DTOs and errors.

## Allowed

- `GraphCalendarGateway : ICalendarGateway` in Infrastructure.
- Application ports returning app DTOs or Result models.
- Failure mapping for throttled, permission denied, token expired, network unavailable, and unknown external failure.

## Not allowed

- ViewModel depends on `GraphServiceClient`.
- Application exposes Graph SDK response types.
- Domain references adapter implementations.
- Raw SDK exceptions bubble to ViewState.

## Preferred pattern

Create a small port around the use case, not a mirror of the entire SDK.

## Anti-pattern

A generic `IGraphClientWrapper` that exposes most of the SDK and becomes an SDK tunnel.

## Agent verification

- Find adapter implementations for each external port.
- Check Graph SDK namespaces are Infrastructure-only.
- Check errors are mapped before reaching Application/Presentation.
