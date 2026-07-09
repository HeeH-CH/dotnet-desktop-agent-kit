# Naming and Folder Conventions

## Intent

Make generated files predictable and keep architecture visible without relying on names alone.

## Applies to

Folders, namespaces, UseCases, ports, adapters, ViewModels, ViewState, and docs.

## Rule

Names should reveal layer, feature, and role. Folder structure should support boundaries but must be backed by correct dependencies.

## Allowed

- `ExampleApp.Application.Calendar.LoadEventsUseCase`.
- `ICalendarGateway` port in Application.
- `GraphCalendarGateway` adapter in Infrastructure.
- `CalendarViewModel` and `CalendarViewState` in App.

## Not allowed

- Ambiguous `Manager`, `Helper`, or `CommonService` for core workflows.
- SDK-derived names leaking into ViewState.
- Public examples with private product names.

## Preferred pattern

Use feature-first names inside each layer and role suffixes when they clarify responsibility.

## Anti-pattern

`Services/GraphService.cs` injected everywhere and used by UI and Application directly.

## Agent verification

- Check type names include feature and role.
- Check namespaces match layer intent.
- Check examples use generic names only.
