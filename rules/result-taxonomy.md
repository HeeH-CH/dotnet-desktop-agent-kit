# Result Taxonomy Rule

## Intent

Make user-visible actions predictable, diagnosable, and safe to present without leaking raw infrastructure details.

## Rule

Do not represent user-visible action outcomes with only `bool`, raw `Exception`, or user-facing `exception.Message`. Use typed results with application-owned status and failure reasons.

## Result should capture

- action kind
- status or severity
- machine-readable failure reason
- retry, reload, or re-authentication hint
- cancellation, stale result, validation failure, conflict, partial success, and permission classification when relevant
- optional diagnostics reference for logs or telemetry
- optional user-facing message key, not raw infrastructure text

## Preferred shape

```text
ActionResult
  ActionKind
  Status
  FailureReason
  RecoveryHint
  DiagnosticsReference
```

Infrastructure adapters translate SDK, HTTP, OS, and persistence failures into application-owned failure reasons. Presentation or App-edge presenters map those reasons to localized user-facing text.

## Violations

- Returning `true` or `false` from a command that can fail in multiple ways.
- Showing `exception.Message` directly to users.
- Passing raw SDK exceptions through ViewState.
- Treating cancellation, stale data, permission denial, validation failure, and transient infrastructure errors as the same failure.

## Agent verification

When adding or refactoring a user-visible action, list its success, cancellation, validation, permission, transient failure, and partial-success outcomes. Use typed results where those outcomes affect presentation or follow-up behavior.
