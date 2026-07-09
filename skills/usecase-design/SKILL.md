---
name: usecase-design
description: Design Application UseCases and ports for desktop user actions.
---

# UseCase Design

## Purpose

Move application orchestration out of ViewModels while avoiding unnecessary layers for trivial UI work.

## When to use

- A command performs IO, validation, branching, or integration.
- A feature needs a reusable application workflow.
- External data is required.

## Inputs

- User intent.
- Current command logic.
- External dependencies.
- Result states.

## Process

1. Name the UseCase by user intent.
2. Define request DTO and cancellation needs.
3. Define response Result and error cases.
4. Define ports for external systems.
5. Keep Domain usage pure.
6. Plan tests with fake ports.

## Output format

UseCase contract, port list, Result model, test plan, and layer placement.

## Anti-patterns

- A generic service with unrelated screen actions.
- Returning external SDK DTOs from UseCases.

## Verification

- UseCase references no UI/Infrastructure.
- Ports are minimal and application-oriented.
- CancellationToken is propagated.

## Related rules

- `rules/usecase-boundaries.md`
- `rules/async-and-cancellation.md`
