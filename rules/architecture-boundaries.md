# Architecture Boundaries

## Intent

Prevent desktop applications from collapsing into UI-driven service code.

## Rule

Keep dependencies flowing inward:

```text
App -> Application -> Domain
Infrastructure -> Application / Domain
Domain -> no external dependencies
```

## Allowed references

- App may reference Application.
- Application may reference Domain.
- Infrastructure may reference Application and Domain.
- Domain should reference only framework-independent primitives and domain-owned types.

## Violations

- Domain references WinUI/WPF.
- Domain references Microsoft Graph SDK.
- Application references Infrastructure implementations.
- ViewModel directly creates HTTP clients, Graph clients, file stores, or database objects.
- Infrastructure types leak into ViewState.

## Agent verification

Check project references, namespaces, constructor dependencies, and type usage. If Roslyn MCP is available, inspect the project graph and references before changing boundaries.
