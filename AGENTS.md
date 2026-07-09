# AGENTS.md

This repository defines an agent skill kit for .NET desktop application development.

## Core objective

Help AI coding agents build and refactor WinUI/WPF desktop applications using MVVM, MVI-style state flow, Clean Architecture, and Roslyn MCP-assisted analysis.

## Core architecture

The default architecture has four conceptual layers:

- App / Presentation
- Application
- Domain
- Infrastructure

Dependency direction must remain inward.

```text
App -> Application -> Domain
Infrastructure -> Application / Domain
Domain -> no external dependencies
```

## Layer responsibilities

### App / Presentation

Owns:

- WinUI/WPF views
- XAML
- code-behind limited to view-only concerns
- ViewModels
- ViewState
- Commands
- Intent dispatching
- UI composition and navigation

Must not own:

- business rules
- Microsoft Graph SDK calls
- persistence logic
- HTTP/file/auth implementation details

### Application

Owns:

- UseCases
- application services
- ports/interfaces for external systems
- DTOs and application models
- orchestration
- validation
- application-level Result models

Must not reference:

- WinUI/WPF types
- Infrastructure implementations
- Microsoft Graph SDK directly

### Domain

Owns:

- pure business concepts
- value objects
- domain rules
- domain models
- domain errors

Must not reference:

- WinUI/WPF
- Microsoft Graph
- HTTP clients
- databases
- file systems
- dependency injection frameworks

### Infrastructure

Owns:

- Microsoft Graph adapter implementations
- authentication adapters
- local storage adapters
- file system adapters
- HTTP clients
- platform-specific service implementations

Infrastructure implements ports defined by Application or Domain.

## Non-negotiable rules

- Do not put business logic in code-behind.
- Do not call Microsoft Graph SDK directly from ViewModels.
- Do not reference WinUI/WPF types from Application or Domain.
- Do not reference Infrastructure from Domain.
- Use Application ports for external systems.
- Use UseCases for user-visible business actions.
- Use ViewState to represent screen state explicitly.
- Use Intent-style methods or commands for user actions.
- Keep each refactoring step buildable.
- Prefer small, reversible changes.

## MVI-style flow

User interaction should follow this flow:

```text
View
 -> Command / Intent
 -> ViewModel
 -> UseCase
 -> Port
 -> Infrastructure Adapter
 -> Result
 -> Reducer / State update
 -> ViewState
 -> View
```

## Roslyn MCP usage

Before large changes, use Roslyn-based analysis where available:

- inspect project dependency graph
- find symbol references
- find implementations of ports
- detect circular dependencies
- inspect diagnostics
- detect dead code
- inspect public API surface

Prefer semantic analysis over blind text search.

## Agent roles

### dotnet-desktop-architect

Use for project structure, architecture boundaries, dependency direction, module placement, and deciding whether a feature belongs in App, Application, Domain, or Infrastructure.

### mvvm-mvi-refactorer

Use for ViewModel cleanup, code-behind removal, ViewState design, Intent design, Command design, and UI state consistency.

### graph-integration-specialist

Use for Microsoft Graph, Planner, Calendar, To Do, authentication, Graph DTO mapping, permission errors, and adapter boundaries.

### quality-auditor

Use for architecture audits, dependency violations, circular dependencies, dead code, naming inconsistencies, missing tests, and refactoring progress reports.

### build-fix-agent

Use for build errors, nullable warnings, package conflicts, project references, and compiler diagnostics.

## Feature development workflow

When adding a new feature:

1. Identify the user action and screen impact.
2. Define the Intent.
3. Define or reuse the ViewState.
4. Decide whether a UseCase is required.
5. If external data is needed, define an Application Port.
6. Implement the Infrastructure Adapter.
7. Wire the ViewModel to the UseCase.
8. Update the View binding.
9. Verify build and dependency direction.
10. Summarize the architectural impact.

## Refactoring workflow

When refactoring existing code:

1. Audit current responsibilities.
2. Identify code-behind logic.
3. Identify ViewModel overreach.
4. Identify direct Infrastructure usage from App/Application.
5. Extract UseCases first.
6. Extract Ports next.
7. Move Graph/file/auth code to Infrastructure.
8. Replace scattered mutable UI flags with explicit ViewState.
9. Keep each step buildable.
10. Document remaining debt.

## Verification output

After any meaningful change, report:

- Build status
- Changed files
- Architecture boundary impact
- ViewModel responsibility changes
- UseCase changes
- Adapter changes
- Known risks
- Follow-up recommendations
