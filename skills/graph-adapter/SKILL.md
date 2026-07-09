---
name: graph-adapter
description: Design Microsoft Graph/M365 integrations behind Application ports and Infrastructure adapters.
---

# Graph Adapter

## Purpose

Keep Graph SDK, auth details, throttling, and external DTOs out of ViewModels and Domain.

## When to use

- Adding Calendar, Planner, To Do, user profile, or auth integration.
- A ViewModel currently calls Graph.
- Raw Graph errors appear in UI.

## Inputs

- User intent and required Graph capability.
- Application UseCase.
- Port candidates.
- Expected failure modes.

## Process

1. Name the Application port by capability, not SDK endpoint.
2. Define minimal request/response DTOs.
3. Model failures: throttled, permission denied, token expired, network unavailable, not found, unknown.
4. Implement adapter in Infrastructure.
5. Map SDK DTOs and exceptions inside the adapter.
6. Return application-level Result to UseCase and ViewModel.
7. Add tests or test plan for mapping and failures.

## Output format

Port/adapter design, DTO mapping, failure model, and verification checklist.

## Anti-patterns

- Creating an `IGraphService` that mirrors the full SDK.
- Letting `GraphServiceClient` or SDK models reach ViewState.
- Using real tenant/client values in docs.

## Verification

- Graph SDK namespaces are Infrastructure-only.
- Application sees only ports and app DTOs.
- ViewState has no external DTOs.

## Related rules

- `rules/infrastructure-adapters.md`
- `rules/public-repo-safety.md`
