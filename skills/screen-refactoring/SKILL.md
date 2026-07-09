---
name: screen-refactoring
description: Refactor a WinUI/WPF screen safely in small buildable steps.
---

# Screen Refactoring

## Purpose

Guide agents through code-behind, binding, ViewModel, and ViewState cleanup without breaking UI behavior silently.

## When to use

- A screen has code-behind logic.
- A ViewModel mixes UI and application concerns.
- A mid-refactor review is needed.

## Inputs

- Target screen files.
- ViewModel and bindings.
- Commands and current errors.

## Process

1. Snapshot responsibilities and bindings.
2. Move code-behind logic to intents where appropriate.
3. Extract UseCases for application flow.
4. Create or normalize ViewState.
5. Update bindings minimally.
6. Verify build after each slice.
7. Document remaining debt.

## Output format

Stepwise refactor log, changed bindings, state model, verification, and risks.

## Anti-patterns

- Rewriting the whole screen at once.
- Changing XAML bindings without tracking property compatibility.

## Verification

- Screen has clear DataContext path.
- Commands map to intents.
- No code-behind business logic remains.

## Related rules

- `rules/winui-codebehind.md`
- `rules/viewmodel-responsibility.md`
