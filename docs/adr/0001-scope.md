# ADR 0001: Scope of dotnet-desktop-agent-kit

## Status

Accepted

## Context

Many .NET AI agent kits focus on ASP.NET Core, Minimal APIs, EF Core, and backend Clean Architecture. Desktop applications have different risks: code-behind logic, ViewModel overreach, UI state complexity, and platform/external SDK leakage.

## Decision

This repository focuses on .NET desktop applications, especially WinUI and WPF, with MVVM, MVI-style state flow, Clean Architecture, and Roslyn MCP-assisted refactoring.

## Consequences

- ASP.NET Core-specific guidance is not the default.
- Examples should be desktop-first.
- External integrations should be described through ports and adapters.
- Agent guidance should emphasize incremental, buildable refactoring.
