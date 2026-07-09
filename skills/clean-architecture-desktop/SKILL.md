---
name: clean-architecture-desktop
description: Apply Clean Architecture to desktop apps without backend-only assumptions.
---

# Clean Architecture Desktop

## Purpose

Translate Clean Architecture into WinUI/WPF realities: Views, ViewModels, UseCases, ports, adapters, and composition root.

## When to use

- A user asks how to structure a desktop app.
- A feature crosses UI and external integrations.
- Application or Domain has UI references.

## Inputs

- Solution/project graph.
- Layer or namespace conventions.
- Target feature.
- Existing adapter and UseCase names.

## Process

1. Identify each layer and current references.
2. Find responsibilities in the wrong layer.
3. Define allowed dependency direction.
4. Move orchestration to Application and external implementations to Infrastructure.
5. Keep Domain pure and small.
6. Document composition-root exceptions.

## Output format

Layering recommendation, dependency diff, migration steps, and verification checks.

## Anti-patterns

- Treating Clean Architecture as only four folders.
- Importing web API endpoint patterns into desktop guidance.
- Creating a full DDD model for simple app state.

## Verification

- Project graph matches allowed direction.
- Application/Domain have no UI/SDK dependencies.
- Composition root is the only broad reference point.

## Related rules

- `rules/architecture-boundaries.md`
- `rules/dependency-injection-composition-root.md`
