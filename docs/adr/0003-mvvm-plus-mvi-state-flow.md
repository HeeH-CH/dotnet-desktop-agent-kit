# ADR: MVVM plus MVI-style State Flow

## Status

Accepted

## Context

Desktop teams often use MVVM but still suffer from scattered state and command logic.

## Decision

Use MVVM for Presentation structure and MVI-style intent/result/ViewState flow for state transitions. Do not present MVVM and MVI as mutually exclusive.

## Consequences

Agents can refactor ViewModels without forcing a new UI framework or pattern migration.
