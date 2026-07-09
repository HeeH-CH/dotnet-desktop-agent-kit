# Async and Cancellation

## Intent

Keep desktop UI responsive and make long-running operations cancelable and failure-aware.

## Applies to

Commands, ViewModel intents, UseCases, ports, adapters, and tests.

## Rule

Async operations crossing ViewModel, UseCase, and adapter boundaries should accept and propagate `CancellationToken`, model cancellation when it affects UI, and avoid blocking the UI thread.

## Allowed

- Async command calls `UseCase.ExecuteAsync(request, cancellationToken)`.
- Adapters pass cancellation to SDK/file/HTTP operations.
- UI-thread dispatch stays in Presentation.

## Not allowed

- `.Result`, `.Wait()`, or blocking sleeps in UI flow.
- Ignoring cancellation passed to UseCases.
- Swallowing exceptions and leaving loading state forever.

## Preferred pattern

Represent loading and cancellation explicitly; handle success, empty, error, and canceled outcomes in reducers.

## Anti-pattern

A command starts async work without awaiting it and leaves exceptions unobserved.

## Agent verification

- Search for blocking async calls.
- Check CancellationToken through UseCase and ports.
- Check loading state exits on error/cancel.
