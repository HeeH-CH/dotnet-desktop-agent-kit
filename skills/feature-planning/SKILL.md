---
name: feature-planning
description: Plan a desktop feature from user intent through ViewState, UseCase, ports, adapter, and verification.
---

# Feature Planning

## Purpose

Create an implementation path that avoids ViewModel and Infrastructure leakage before coding begins.

## When to use

- Starting a new screen or feature.
- Expanding an existing feature.
- Asking for architecture selection before implementation.

## Inputs

- Feature name and target framework.
- Screen impact and data/integration needs.
- Constraints and acceptance criteria.

## Process

1. Define the user-visible intent.
2. Sketch ViewState states.
3. Decide if a UseCase is required.
4. List ports and adapters for IO.
5. Identify affected files.
6. Plan tests and verification.
7. Call out public-safety constraints for examples.

## Output format

Feature plan with flow diagram, file list, risk list, and acceptance checks.

## Anti-patterns

- Starting with SDK code before defining ViewState and UseCase.
- Adding backend-only assumptions.

## Verification

- Plan maps every user action to state outcome.
- External calls cross a port.
- Tests cover success and failure.

## Related rules

- `rules/mvi-state-flow.md`
- `rules/usecase-boundaries.md`
