# Workflow: Add Graph Integration

## Goal

Add Microsoft Graph/M365 capability through Application ports and Infrastructure adapters.

## When to use

Calendar, Planner, To Do, profile, auth, or similar M365 data is needed.

## Inputs

- Capability required.
- Conceptual permissions, without real tenant details.
- UseCase that needs the data.
- Failure states required by UI.

## Steps

1. Load Graph specialist and Graph adapter skill.
2. Define minimal Application port.
3. Define app DTOs and Result errors.
4. Implement Infrastructure adapter with Graph SDK isolated.
5. Map SDK DTOs to Application DTOs.
6. Map throttling, permission denied, token expired, network unavailable, and unknown failures.
7. Update UseCase and ViewModel.
8. Add tests for mapping and failure handling.
9. Run public-safety scan.

## Roslyn MCP checks

- Graph SDK namespace references.
- Port implementations.
- ViewState DTO leakage check.
- Diagnostics.

## Expected file changes

- Application port/DTO/Result.
- Infrastructure Graph adapter.
- UseCase update.
- ViewModel state mapping.
- Adapter tests.

## Verification

| Check | Result | Notes |
|---|---|---|
| Graph SDK isolation | pass/fail | Infrastructure only |
| Failure mapping | pass/fail | modeled errors |
| Public safety | pass/fail | no real tenant data |

## Final report format

Port, adapter, failure model, changed files, verification, and risks.
