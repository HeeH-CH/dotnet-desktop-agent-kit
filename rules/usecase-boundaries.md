# UseCase Boundaries

## Intent

Use Application UseCases for meaningful user-visible workflows without over-layering trivial UI work.

## Applies to

UseCases, application services, request/response models, and ports.

## Rule

Create a UseCase when a user action involves IO, validation, branching, orchestration, authorization decisions, or reusable application behavior.

## Allowed

- `LoadCalendarEventsUseCase` orchestrates a gateway and returns Result.
- UseCase accepts request DTO plus `CancellationToken`.
- UseCase calls ports, not adapters.

## Not allowed

- UseCase references WinUI/WPF or ViewModel.
- UseCase returns Graph SDK DTOs.
- UseCase constructs Infrastructure adapters.

## Preferred pattern

Design UseCases around user intent and application outcome.

## Anti-pattern

One large `DesktopService` with every screen action and every adapter dependency.

## Agent verification

- Check inputs/outputs are Application models.
- Check no UI/Infrastructure references.
- Check cancellation is accepted and forwarded.
