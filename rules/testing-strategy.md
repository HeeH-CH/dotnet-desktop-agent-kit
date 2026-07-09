# Testing Strategy

## Intent

Make desktop architecture testable without requiring fragile UI automation for every behavior.

## Applies to

Domain rules, UseCases, ViewModels, reducers, adapters, contract tests, and docs examples.

## Rule

Prefer fast tests around UseCases, ViewState reducers, and adapter mappings. Use UI automation selectively for binding/navigation smoke tests.

## Allowed

- UseCase tests with fake ports.
- ViewModel tests verifying intent-to-ViewState transitions.
- Adapter mapping tests with sanitized sample DTOs.
- Contract tests for failure modeling.

## Not allowed

- Only manual UI testing for application flow.
- Tests that call real tenants or external accounts.
- Snapshot tests containing private data.

## Preferred pattern

Test the flow at the lowest stable boundary: Domain, UseCase, ViewModel state transition, adapter mapping.

## Anti-pattern

A suite that can pass while a ViewModel directly calls Graph SDK.

## Agent verification

- Check UseCase success/failure coverage.
- Check ViewModel loading/error state tests.
- Check no tests require real credentials.
