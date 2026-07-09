---
name: desktop-result-taxonomy
description: Designs typed action results and failure taxonomies for .NET desktop applications. Use when replacing bool returns, raw exceptions, exception.Message display, ad hoc status strings, or mixed Application/Presentation error handling with machine-readable Application results and user-facing Presentation text.
---

# Desktop Result Taxonomy

## Load first

Read these rule files when present:

- `../../rules/result-taxonomy.md`
- `../../rules/architecture-boundaries.md`
- `../../rules/infrastructure-adapters.md`

If a rule file is unavailable, apply this skill and the local project conventions.

## Separation rule

Application returns machine-readable results. Presentation creates user-facing text.

Application result data should be stable, testable, and localization-neutral. Presentation, App-edge presenters, or ViewModels may map that data to user-facing labels, descriptions, dialogs, toasts, or inline messages.

## Recommended result shape

Use project naming conventions, but preserve these concepts:

- action kind
- status or severity
- machine-readable failure reason
- retry, reload, sign-in, permission, or contact-support hint
- optional diagnostics log reference
- optional stale, cancelled, timeout, throttled, conflict, validation, or partial-success classification
- optional typed payload for success

Example categories:

```text
Success
PartialSuccess
Cancelled
ValidationFailed
PermissionDenied
AuthenticationRequired
NetworkUnavailable
Throttled
NotFound
Conflict
ExternalServiceFailed
UnexpectedFailure
```

## Layer responsibilities

Infrastructure:

- catch SDK-specific exceptions at adapter boundaries
- map external failures to application-owned reasons
- include diagnostics references when useful
- avoid leaking SDK exception types inward

Application:

- return typed results from use cases
- preserve action kind, status, failure reason, and recovery hints
- avoid localized strings and UI instructions

Presentation/App edge:

- map machine-readable results to user-facing text
- choose UI surfaces such as inline error, dialog, toast, or retry button
- handle localization and tone
- avoid branching on raw exception messages

## Replacement workflow

1. Find `bool`, `Exception`, `exception.Message`, magic status strings, and nullable result patterns.
2. Identify the user-visible action being represented.
3. Define a small taxonomy for that action family before adding broad global types.
4. Map infrastructure failures once at the adapter or gateway boundary.
5. Update Application to return typed results.
6. Update Presentation to translate results into user-facing text.
7. Add targeted tests when the change affects permissions, deletion, overwrite, auth, or data loss.

## Anti-patterns

- Returning `false` without a failure reason.
- Displaying `exception.Message` directly to users.
- Putting localized UI text in Application or Domain result types.
- Allowing ViewModels to know Graph, MSAL, database, or HTTP exception classes.
- Treating cancellation, stale data, partial success, and external failure as the same generic error.
