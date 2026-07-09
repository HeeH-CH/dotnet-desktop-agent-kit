# Error Learning Rule

## Intent

Preserve useful lessons from real failures so future agents do not rediscover the same root cause.

## Rule

When an investigated or fixed error is likely to recur, record a concise agent-facing note in the repository's agent documentation area, such as `.devs/`, `.codex/`, or another project-approved location.

## Record only useful lessons

Good notes explain:

- symptom
- root cause
- fix
- verification command
- remaining risk, if any

Avoid noisy logs, speculation, full stack traces without interpretation, and product-specific details that are not needed to prevent recurrence.

## When to write a note

- build or compiler issue caused by a non-obvious project convention
- recurring WinUI, Windows App SDK, packaging, threading, binding, or interop failure
- dependency, SDK, or tooling mismatch
- architecture boundary mistake that caused a bug
- verification trap that future agents are likely to hit

## When not to write a note

- trivial typo
- one-off local environment issue
- unrelated failing test that was not investigated
- temporary command output without a durable lesson

## Agent verification

After fixing a non-trivial error, decide whether the lesson would save a future agent time. If yes, add or update the smallest relevant agent-facing note and mention it in the final report.
