---
name: clean-architecture-desktop
description: Applies Clean Architecture to .NET desktop applications without assuming ASP.NET Core or web APIs.
---

# Clean Architecture for Desktop Apps

## Core idea

Desktop Clean Architecture uses App / Application / Domain / Infrastructure instead of Api / Application / Domain / Infrastructure.

```text
App / Presentation -> Application -> Domain
Infrastructure -> Application / Domain
```

## Layer mapping

### App / Presentation

- WinUI/WPF Views
- ViewModels
- ViewState
- Commands
- navigation
- composition root

### Application

- UseCases
- ports
- validation
- orchestration
- application DTOs
- Result models

### Domain

- pure business models
- invariants
- value objects
- domain errors

### Infrastructure

- Microsoft Graph
- authentication
- local storage
- file system
- HTTP APIs
- platform adapters

## UseCase guidance

Create a UseCase when:

- the action is user-visible and meaningful
- the flow touches external systems
- the ViewModel would otherwise become orchestration-heavy
- the flow should be testable without UI

Avoid UseCases for trivial UI-only state toggles.

## Port guidance

Create an Application port when:

- Application needs data from an external system
- the implementation may change
- the dependency is hard to test directly
- SDK types would otherwise leak inward

## Verification

- Domain has no framework references.
- Application has no Infrastructure references.
- ViewModels depend on UseCases, not SDK clients.
- Infrastructure implements ports.
- External DTOs do not leak into ViewState.
