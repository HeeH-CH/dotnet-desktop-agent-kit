---
name: mvi-reducer-store
description: Designs and audits MVI-style reducer and store boundaries for .NET desktop apps. Use when implementing or refactoring intents, reducers, stores, ViewState publication, command dispatch, async effects, or MVVM-to-MVI screen flows.
---

# MVI Reducer and Store

## Load first

Read these rule files when present:

- `../../rules/mvi-state-flow.md`
- `../../rules/architecture-boundaries.md`
- `../../rules/app-edge-boundaries.md`

If a rule file is unavailable, apply this skill and the local project conventions.

## Core boundary

Reducers are pure. Stores dispatch and publish state. Side effects live outside reducers and stores.

```text
View command -> Intent -> Store dispatch -> Reducer -> State
Effect/controller/use case -> Result intent -> Store dispatch -> Reducer -> State
```

## Reducer rules

Reducers may:

- accept current state and an intent/result
- return the next state
- perform deterministic, in-memory transformations
- derive flags such as loading, empty, selected, stale, cancelled, or partial

Reducers must not:

- perform async work
- call file, database, HTTP, Graph, auth, clipboard, process, or OS APIs
- mutate WinUI controls or platform handles
- create dialogs, toasts, navigation, or focus changes
- catch raw infrastructure exceptions as control flow

## Store rules

Stores may:

- serialize dispatch
- call the reducer
- hold the latest immutable or replaceable state
- publish state changes to subscribers or bindable surfaces

Stores must not:

- perform external side effects
- own SDK clients, repositories, use cases, or platform services
- contain business workflows that belong in effects/controllers/use cases
- translate failures into user-facing text

## Side effect placement

Put async and external work in a named boundary:

- ViewModel intent handler for small UI-only orchestration
- controller/effect for screen-specific async flows
- Application use case for meaningful user-visible workflows
- Infrastructure adapter behind an Application port for external systems
- App-edge presenter for dialogs, navigation, clipboard, and platform UI actions

Return side effect outcomes as typed results or result intents, then reduce them into state.

## Audit checklist

- Reducer methods are synchronous and deterministic.
- Reducer tests can run without mocks for SDKs, UI controls, file I/O, or network.
- Store has no infrastructure dependencies.
- Every async workflow has a named owner outside reducer/store.
- Failure data entering the reducer is machine-readable, not raw `Exception.Message` or localized UI text.
