# ADR: Roslyn MCP-first Analysis

## Status

Accepted

## Context

C# refactors need semantic evidence beyond text search.

## Decision

When available, agents should use Roslyn MCP for project graph, references, implementations, diagnostics, cycles, dead code, public API surface, and leakage checks.

## Consequences

Refactors become safer and final reports can cite concrete analysis results.
