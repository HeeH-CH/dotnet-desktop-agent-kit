---
name: testing-strategy
description: Choose tests for UseCases, ViewModels, reducers, adapters, and desktop smoke checks.
---

# Testing Strategy

## Purpose

Keep desktop behavior testable without relying only on fragile UI automation.

## When to use

- Adding or refactoring UseCases, ViewModels, adapters, or Graph integration.
- Final verification needs test coverage guidance.

## Inputs

- Changed layers.
- Available test projects.
- Target behaviors.
- External dependencies.

## Process

1. Identify behavior by layer.
2. Use fake ports for UseCase tests.
3. Test ViewModel intent-to-ViewState transitions.
4. Test adapter DTO/error mapping with sanitized data.
5. Recommend UI automation only for critical binding/navigation smoke paths.
6. Avoid real tenants, accounts, and secrets.

## Output format

Test matrix with layer, behavior, test type, fake/stub needs, and commands.

## Anti-patterns

- Testing only through UI automation.
- Calling real Graph/M365 in unit tests.

## Verification

- Success/failure/cancel paths covered.
- Tests do not require secrets.
- Boundary violations would be visible.

## Related rules

- `rules/testing-strategy.md`
- `rules/public-repo-safety.md`
