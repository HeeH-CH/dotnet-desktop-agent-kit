---
name: mvvm-mvi-refactoring
description: Refactors WinUI/WPF screens toward clean MVVM and MVI-style state flow.
---

# MVVM + MVI Refactoring

## Purpose

Use this skill when code-behind is too large, ViewModels are doing too much, or UI state is scattered.

## Target shape

```text
View -> Command / Intent -> ViewModel -> UseCase -> Result -> ViewState
```

## Refactoring steps

1. List current code-behind responsibilities.
2. Move user actions into commands or intent methods.
3. Identify async workflows and extract UseCases.
4. Replace scattered UI flags with a ViewState model.
5. Make loading, error, empty, and success states explicit.
6. Ensure ViewModel does not call external SDKs directly.
7. Keep each step buildable.

## ViewModel responsibilities

Allowed:

- expose ViewState
- expose commands
- dispatch intents
- call UseCases
- translate UseCase results into ViewState

Not allowed:

- call Microsoft Graph directly
- own business rules
- own persistence details
- own file/auth/http implementation details

## Output format

```markdown
## MVVM/MVI Refactoring Plan

### Current problems
- ...

### Proposed state flow
- Intent: ...
- UseCase: ...
- Result: ...
- ViewState: ...

### Steps
1. ...

### Verification
- ...
```
