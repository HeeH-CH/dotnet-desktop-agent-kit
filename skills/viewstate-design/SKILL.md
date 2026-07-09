---
name: viewstate-design
description: Design ViewState models for WinUI/WPF screens using MVI-style state flow.
---

# ViewState Design

## Purpose

Create a single explicit screen state that bindings can observe and reducers can update.

## When to use

- Screen has many flags.
- New feature needs loading/error/empty/success states.
- External DTOs are exposed in UI state.

## Inputs

- Screen behavior.
- XAML binding needs.
- UseCase Result states.
- Design-time data needs.

## Process

1. List all visible UI states.
2. Define data needed by each state.
3. Choose a record/class shape compatible with MVVM toolkit.
4. Map application DTOs to presentation-safe data.
5. Define reducer methods for Result mapping.
6. Check invalid state combinations.

## Output format

ViewState shape, state transition table, binding notes, and verification checklist.

## Anti-patterns

- A ViewState that contains Graph SDK models.
- Boolean flag combinations that permit impossible UI states.

## Verification

- Every UI branch has a state.
- Invalid combinations are removed or documented.
- Bindings use presentation-safe properties.

## Related rules

- `rules/mvi-state-flow.md`
- `rules/viewmodel-responsibility.md`
