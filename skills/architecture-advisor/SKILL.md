---
name: architecture-advisor
description: Choose layer placement, dependency direction, and desktop Clean Architecture boundaries for WinUI/WPF work.
---

# Architecture Advisor

## Purpose

Decide where a feature, type, dependency, or responsibility belongs before editing code.

## When to use

- A feature touches more than one layer.
- A ViewModel is gaining dependencies.
- A project reference or namespace change is proposed.

## Inputs

- Feature or refactor description.
- Current project/folder structure.
- Target framework and integrations.
- Build or Roslyn MCP findings.

## Process

1. Restate the user intent and affected screen/feature.
2. Classify each responsibility as App, Application, Domain, or Infrastructure.
3. Identify ports needed for external systems.
4. Check dependency direction before proposing files.
5. Prefer a small, reversible change plan.
6. List verification commands and Roslyn MCP checks.

## Output format

Decision, file placement table, dependency impact, risks, and verification checklist.

## Anti-patterns

- Choosing folders without checking references.
- Putting SDK calls in ViewModels.
- Over-designing Domain when the behavior is application orchestration.

## Verification

- Boundary table has no forbidden dependency.
- UseCases and ports are named by user intent.
- Infrastructure adapters are isolated.

## Related rules

- `rules/architecture-boundaries.md`
- `rules/usecase-boundaries.md`
- `rules/infrastructure-adapters.md`
