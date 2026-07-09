---
name: mvvm-mvi-refactoring
description: Refactor ViewModels toward explicit Intent -> UseCase -> Result -> ViewState flow.
---

# MVVM MVI Refactoring

## Purpose

Turn scattered command logic and mutable UI flags into clear state transitions while preserving MVVM.

## When to use

- A ViewModel has many services or flags.
- Commands contain IO, SDK calls, or business branching.
- UI state has invalid combinations.

## Inputs

- Target ViewModel and XAML bindings.
- Current commands and observable properties.
- Available UseCases and ports.

## Process

1. Inventory commands, properties, and injected services.
2. Group user actions into intents.
3. Design or normalize ViewState.
4. Extract application work to UseCases.
5. Map UseCase Result to ViewState in reducer-style methods.
6. Preserve bindings or document required binding changes.
7. Run build and ViewModel tests.

## Output format

Refactor plan, before/after responsibility table, changed state model, and verification result.

## Anti-patterns

- Moving all logic into a bigger ViewModel.
- Using ViewState as a bag of SDK DTOs.
- Breaking bindings without documenting XAML changes.

## Verification

- Commands are intent-focused.
- No Graph SDK or Infrastructure adapter in ViewModel.
- Loading/error/empty states are representable.

## Related rules

- `rules/mvi-state-flow.md`
- `rules/viewmodel-responsibility.md`
- `rules/winui-codebehind.md`
