# Workflow: Introduce UseCase

## Goal

Extract a user-visible workflow from ViewModel or service code into an Application UseCase.

## When to use

A command has validation, branching, IO, integration calls, or reusable application behavior.

## Inputs

- Source logic location.
- User intent.
- Input/output data.
- External dependencies.

## Steps

1. Name the UseCase by user intent.
2. Define request DTO and Result response.
3. Define needed ports.
4. Move orchestration into Application.
5. Map errors into application-level Result.
6. Update ViewModel to call UseCase.
7. Add tests with fake ports.
8. Verify no UI/Infrastructure references in UseCase.

## Roslyn MCP checks

- Symbol references before move.
- Diagnostics after extraction.
- Port implementation references.

## Expected file changes

- Application UseCase.
- Application DTO/Result/port.
- Updated ViewModel.
- Tests.

## Verification

| Check | Result | Notes |
|---|---|---|
| UseCase dependencies | pass/fail | UI/Infrastructure references |
| ViewModel responsibility | pass/fail | command reduced |
| Tests | pass/fail/not run | fake ports |

## Final report format

UseCase contract, moved responsibility, changed files, verification, risks.
