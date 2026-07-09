# AGENTS.md

This repository defines an agent skill kit for .NET desktop application development.

## Core objective

Help AI coding agents build and refactor WinUI/WPF desktop applications using MVVM, MVI-style state flow, Clean Architecture, and Roslyn MCP-assisted analysis.

The kit is generic. Do not encode product-specific tenant, workspace, account, or organization details in reusable guidance.

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

WinUI 3 and Windows App SDK are the default desktop target for new Windows guidance. WPF remains supported when a project is WPF, when the user asks for WPF, or when migration/comparison work requires it.

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
- App-edge authority for windows, dialogs, focus, clipboard, process launch, file pickers, and interactive auth surfaces

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

## Operating guide

Use the reusable rules, workflows, and skills in this kit when they exist. Bundle-specific documents may be added over time; prefer the most specific local file before falling back to this summary.

- Read `rules/architecture-boundaries.md` for layer ownership and dependency direction.
- Read `rules/winui-codebehind.md` for view-only code-behind constraints.
- Read `rules/mvi-state-flow.md` for intent, reducer, store, and ViewState rules.
- Read `rules/infrastructure-adapters.md` before touching external SDK, file, network, auth, or storage adapters.
- Read `rules/app-edge-boundaries.md` for WinUI/WPF platform authority that must stay at the App edge.
- Read `rules/result-taxonomy.md` before modeling user-visible action outcomes or external failure mapping.
- Read `rules/parallel-wave.md` for broad multi-area refactoring.
- Read `rules/error-learning.md` after fixing a repeatable failure.
- Use `workflows/parallel-wave.md` for broad architecture or refactoring changes.
- Use `workflows/refactor-screen.md` for View, ViewModel, state, use case, and adapter cleanup.
- Use `workflows/verify-change.md` for scoped verification planning.
- Use `workflows/runtime-smoke.md` only when an interactive desktop smoke check is needed.
- Use `skills/winui-app-edge-boundaries/SKILL.md` for window, XAML, dialog, platform handle, auth surface, and local OS authority decisions.
- Use `skills/mvi-reducer-store/SKILL.md` for reducer/store purity and intent/result flow.
- Use `skills/desktop-result-taxonomy/SKILL.md` for typed user-visible operation results.
- Use `skills/desktop-composition-di/SKILL.md` for dependency injection and composition root decisions.

## Tool and skill routing

Use installed tools and skills in this order when they are available:

- WinUI 3, Windows App SDK, XAML, binding, theming, packaging, UI testing, WPF migration, and Fluent design: winui plugin skills.
- CommunityToolkit.Mvvm ViewModels, `[ObservableProperty]`, `[RelayCommand]`, validation, and command generation: `mvvm-toolkit`.
- CommunityToolkit.Mvvm with dependency injection and `Microsoft.Extensions.DependencyInjection`: `mvvm-toolkit-di`.
- CommunityToolkit.Mvvm messenger patterns: `mvvm-toolkit-messenger`.
- Microsoft concepts, setup, limits, configuration, Windows App SDK, MSAL, Microsoft Graph, .NET, and official platform behavior: `microsoft-docs`, `microsoft-code-reference`, and the `microsoft-learn` MCP server.
- C# semantic analysis, symbol/reference navigation, generated partial ViewModel relationships, diagnostics, and safe refactoring impact checks: the `roslyn` MCP server.
- External library or API documentation, framework setup, migrations, package-specific behavior, and code examples: Context7 MCP. Resolve the library ID first unless the user already provided it.

If a preferred tool is unavailable, state that briefly and fall back to official documentation, existing project patterns, and targeted text search.

## App-edge authority

Keep platform and UI authority at the App edge. ViewModels, Application, and Domain must not directly own or require:

- `Window`, `XamlRoot`, `AppWindow`, `DispatcherQueue`, raw HWND, DWM/User32 interop, or similar platform handles.
- Dialog, flyout, focus, pointer capture, keyboard routing, tray, storyboard, timer, or visual tree mutation authority.
- Clipboard, file picker, process launch, shell integration, local OS integration, or native window placement authority.
- MSAL/WAM parent-window routing or interactive authentication surfaces.

Pass App-edge decisions through presenters, coordinators, factories, or ports that expose application-owned abstractions rather than raw platform types.

## Result taxonomy

User-visible operations should return typed results instead of plain `bool`, raw `Exception`, or direct `exception.Message` strings.

Prefer result models that include:

- action kind
- status or severity
- machine-readable failure reason
- retry, reload, stale, cancelled, or partial-success classification when relevant
- optional diagnostics log reference
- optional user-message key or presentation hint

Infrastructure should translate SDK, OS, network, auth, and storage failures into application-owned failure reasons. Presentation or App-edge presenters map those reasons to user-facing text.

## Non-negotiable rules

- Do not put business logic in code-behind.
- Do not call Microsoft Graph SDK directly from ViewModels.
- Do not reference WinUI/WPF types from Application or Domain.
- Do not move App-edge authority into ViewModels, Application, or Domain.
- Do not reference Infrastructure from Domain.
- Use Application ports for external systems.
- Use UseCases for user-visible business actions.
- Use typed result taxonomy for user-visible action outcomes.
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

Reducers and stores must stay pure. Reducers compute next state from current state plus intent/result. Stores dispatch and publish state. Async I/O, HTTP, SDK calls, database work, file access, and WinUI control mutation belong outside reducer/store boundaries.

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

Load the relevant solution or workspace before relying on Roslyn answers. Treat Roslyn output as static analysis support, not a substitute for targeted build or test verification.

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

For broad or risky refactors, use a wave-based workflow:

1. Plan the full local flow and ownership bundles.
2. Run read-only discovery and audit in parallel when ownership is disjoint.
3. Implement scoped batches by owner bundle.
4. Re-audit against the original plan, changed files, and architecture rules.
5. Run the narrowest meaningful verification once the batch is internally consistent.
6. Fix blocking audit or verification findings and re-audit narrowly.

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
