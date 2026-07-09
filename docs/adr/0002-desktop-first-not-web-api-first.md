# ADR: Desktop-first, not Web API-first

## Status

Accepted

## Context

Most .NET architecture guidance is backend oriented, but this kit targets desktop-specific failure modes.

## Decision

Guidance must prioritize WinUI/WPF, code-behind boundaries, ViewModel responsibility, ViewState, desktop integration, and Roslyn MCP audits. Backend-only ASP.NET Core assumptions are out of scope.

## Consequences

The repository remains distinct from backend Clean Architecture templates.
