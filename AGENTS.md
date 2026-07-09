# AGENTS.md

This repository defines the operating doctrine for a public, copyable .NET desktop AI coding-agent skill kit.

## Core objective

Help AI coding agents build, extend, audit, and refactor WinUI/WPF desktop applications using MVVM, MVI-style intent/result/ViewState flow, Clean Architecture, Application UseCases and ports, Infrastructure adapters, and Roslyn MCP-assisted semantic analysis.

The kit is generic. Do not encode product-specific tenant, workspace, account, organization, internal URL, or customer details in reusable guidance.

## Architecture doctrine

Keep the app shell thin. Keep ViewModels focused on state and user intents. Put business/application workflows in Application UseCases. Define external system boundaries as Application ports. Implement those ports in Infrastructure. Keep Domain pure.

```text
View -> Command / Intent -> ViewModel -> UseCase -> Port -> Infrastructure Adapter -> Result -> Reducer / State update -> ViewState -> View
```

Dependency direction is non-negotiable:

```text
App -> Application -> Domain
Infrastructure -> Application / Domain
Domain -> no external dependencies
```

## Layer responsibilities

### App / Presentation

Owns WinUI/WPF Views, XAML, UI-only resources, ViewModels, ViewState, commands, intent dispatching, navigation, UI composition, and App-edge authority for windows, dialogs, focus, clipboard, process launch, file pickers, native handles, and interactive auth surfaces. It must not own business rules, Graph SDK calls, persistence implementation, or raw external SDK DTOs in ViewState.

### Application

Owns UseCases, ports/interfaces such as `ICalendarGateway`, `IPlannerGateway`, `ITodoGateway`, `IUserProfileGateway`, `IAuthTokenProvider`, request/response DTOs, orchestration, validation, cancellation propagation, and application-level Result/Error models. It must not reference WinUI/WPF, Infrastructure implementations, Microsoft Graph SDK, ViewModels, or XAML concepts.

### Domain

Owns pure business concepts, value objects, domain rules, framework-independent models, and domain errors. It must not reference Presentation, Application implementation details, Infrastructure, SDKs, databases, file systems, OS APIs, or DI containers.

### Infrastructure

Owns Microsoft Graph adapter implementations, authentication/token providers, local storage, file access, external API clients, and mapping from external DTOs/exceptions to Application DTOs/errors. Infrastructure implements ports defined by Application or Domain and must not define UI state.

## Operating guide

Use the reusable rules, workflows, and skills in this kit when they exist. Prefer the most specific local file before falling back to this summary.

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

## Non-negotiable rules

- Do not put business logic in code-behind.
- Do not call Microsoft Graph SDK directly from ViewModels.
- Do not reference WinUI/WPF types from Application or Domain.
- Do not move App-edge authority into ViewModels, Application, or Domain.
- Do not reference Infrastructure from Domain.
- Do not expose external SDK DTOs in ViewState.
- Do not treat Clean Architecture as folder naming only.
- Do not introduce backend-only ASP.NET Core assumptions into desktop guidance.
- Use Application ports for external systems.
- Use UseCases for user-visible actions that involve IO, validation, branching, integration, or orchestration.
- Use typed result taxonomy for user-visible action outcomes.
- Use ViewState to represent screen state explicitly.
- Use Intent-style methods or commands for user actions.
- Propagate `CancellationToken` through async UseCase and adapter calls.
- Keep each refactoring step buildable.
- Prefer small, reversible changes.
- Keep examples generic and public-safe.

## Allowed and disallowed dependencies

| From | Allowed | Not allowed |
|---|---|---|
| App / Presentation | Application, Domain, UI framework, CommunityToolkit.Mvvm | Graph SDK in ViewModels; business calls to Infrastructure implementations |
| Application | Domain, BCL abstractions, application ports | WinUI/WPF, Infrastructure, Graph SDK, external SDK DTO contracts |
| Domain | BCL and domain-owned types | Application, Infrastructure, UI, SDKs, DI containers |
| Infrastructure | Application, Domain, external SDKs, OS/file/auth APIs | App/ViewModel references, ViewState, UI controls |

## MVI-style flow

1. View raises a command or event.
2. ViewModel converts it to an explicit intent method.
3. ViewModel updates ViewState to loading/optimistic state.
4. ViewModel calls an Application UseCase.
5. UseCase calls ports and returns Result.
6. ViewModel reduces Result into ViewState.
7. View observes ViewState through binding.

## Roslyn MCP usage policy

When Roslyn MCP is available, prefer it before broad textual edits for C# code. Check project graph, symbol references, port/interface implementations, circular dependencies, diagnostics, dead code, public API surface, ViewModel references to Infrastructure or Graph SDK namespaces, Application/Domain references to WinUI/WPF namespaces, and Infrastructure DTO leakage into ViewState.

Reducers and stores must stay pure. Reducers compute next state from current state plus intent/result. Stores dispatch and publish state. Async I/O, HTTP, SDK calls, database work, file access, and WinUI control mutation belong outside reducer/store boundaries.

If Roslyn MCP is unavailable, fall back to compiler diagnostics, `dotnet build`, `dotnet test`, and targeted text search. Report that semantic checks were unavailable.

## Agent routing table

| Situation | Primary agent |
|---|---|
| Choose architecture or layer placement | `agents/dotnet-desktop-architect.md` |
| Clean ViewModel or code-behind | `agents/mvvm-mvi-refactorer.md` |
| Add Microsoft Graph/M365 integration | `agents/graph-integration-specialist.md` |
| Fix build or project references | `agents/build-fix-agent.md` |
| Review UI state correctness | `agents/ui-state-reviewer.md` |
| Design test strategy | `agents/test-strategy-agent.md` |
| Maintain docs, rules, or workflows | `agents/documentation-maintainer.md` |
| Audit after refactor | `agents/quality-auditor.md` |

## Skill loading guide

Load only the skills needed for the task. Feature work usually uses `skills/feature-planning/SKILL.md`, `skills/usecase-design/SKILL.md`, and `skills/viewstate-design/SKILL.md`. Refactoring usually uses `skills/mvvm-mvi-refactoring/SKILL.md`, `skills/screen-refactoring/SKILL.md`, and `skills/verification/SKILL.md`. Graph work uses `skills/graph-adapter/SKILL.md`. Audits use `skills/roslyn-mcp-audit/SKILL.md`.

For app-edge concerns, use `skills/winui-app-edge-boundaries/SKILL.md`. For reducer/store design, use `skills/mvi-reducer-store/SKILL.md`. For user-visible result modeling, use `skills/desktop-result-taxonomy/SKILL.md`. For composition root and DI boundaries, use `skills/desktop-composition-di/SKILL.md`.

## Feature development workflow

1. Identify the screen, user intent, and resulting state changes.
2. Load `workflows/add-feature.md`.
3. Decide whether the feature needs a UseCase.
4. Define Application request/response models and ports before Infrastructure.
5. Keep external SDK DTOs inside Infrastructure.
6. Update ViewModel intents and ViewState.
7. Bind the View to ViewState.
8. Verify architecture, build, tests, links, and public safety.

## Refactoring workflow

1. Load `workflows/refactor-screen.md` or `workflows/migrate-code-behind.md`.
2. Audit current responsibilities before editing.
3. Use Roslyn MCP to find references and dependency violations when available.
4. Move business/application flow to UseCases.
5. Move SDK/file/auth/local-storage code to Infrastructure adapters.
6. Replace scattered state flags with ViewState.
7. Keep changes small and reversible.
8. Document remaining debt.

## Verification output format

For broad or risky refactors, use a wave-based workflow:

1. Plan the full local flow and ownership bundles.
2. Run read-only discovery and audit in parallel when ownership is disjoint.
3. Implement scoped batches by owner bundle.
4. Re-audit against the original plan, changed files, and architecture rules.
5. Run the narrowest meaningful verification once the batch is internally consistent.
6. Fix blocking audit or verification findings and re-audit narrowly.

```markdown
## Verification

| Check | Result | Notes |
|---|---|---|
| Build | pass/fail/not run | command and important output |
| Tests | pass/fail/not run | scope |
| Roslyn MCP | pass/fail/not available | project graph, references, diagnostics |
| Architecture boundaries | pass/fail | violations or none |
| ViewState/Intent flow | pass/fail | screen impact |
| Public safety | pass/fail | sensitive info check |
```

## Public repo safety rules

Never include company names, internal product names, tenant IDs, client secrets, real client IDs, private redirect URIs, private M365 organization details, private email addresses, production URLs, internal endpoints, screenshots with private data, or secrets hidden in examples. Use generic names such as `ExampleApp`, `ExampleGraphAdapter`, `YOUR_TENANT_ID`, `YOUR_CLIENT_ID`, and `example.invalid`.
