# Roslyn MCP for Desktop Refactoring

Roslyn MCP is important for this kit because C# desktop refactors are often unsafe with text search alone. XAML bindings, ViewModel commands, project references, and SDK namespaces need semantic checks.

This repository does not implement a Roslyn MCP server. It defines how agents should use one when available.

## Use Roslyn MCP before risky edits

Prefer semantic checks for moving or renaming ViewModels, UseCases, ports, adapters, or DTOs; extracting code-behind logic; changing project references; removing unused code; and checking SDK/UI leakage across layers.

## Required analysis items

### Project graph

Verify `App -> Application -> Domain`, `Infrastructure -> Application / Domain`, and `Domain -> no external dependencies`.

### Symbol references

Before moving or renaming a type, find references and update call sites deliberately. Review XAML-bound property and command names even when semantic tools cannot fully see XAML.

### Port/interface implementations

For each Application port such as `ICalendarGateway`, find implementations. They should be in Infrastructure or tests, not Presentation.

### Circular dependencies

Detect cycles between projects and namespaces.

### Diagnostics

Check compiler diagnostics and nullable warnings before and after refactors.

### Dead code

Find unused UseCases, ViewModels, ports, adapters, and DTOs. Confirm before deleting public API surface or XAML-bound members.

### Public API surface

When changing public interfaces or DTOs, list impacted consumers and compatibility risk.

## Desktop-specific leakage checks

Agents should detect ViewModels referencing Infrastructure namespaces or `Microsoft.Graph`; Application or Domain referencing `Microsoft.UI.Xaml`, `System.Windows`, or other UI types; Domain referencing Infrastructure, IO, HTTP, database, or DI packages; Infrastructure DTOs in ViewState; and raw SDK exceptions exposed as UI state.

## Fallback when MCP is unavailable

Report the limitation and use `dotnet build`, `dotnet test`, targeted namespace search, project file reference inspection, and manual XAML binding review. Do not claim semantic verification if only text search was used.
