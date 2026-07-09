# Parallel Wave Rule

## Intent

Use parallel agents without losing ownership clarity, architectural direction, or review quality.

## Rule

Parallel work is allowed for broad discovery, read-only audit, disjoint implementation bundles, and re-audit. Do not edit the same file, tightly coupled reducer/store/ViewModel bundle, or shared contract concurrently.

## Preferred wave

```text
plan -> parallel discovery/audit -> scoped implementation -> integration -> re-audit -> verification
```

The main agent owns the plan, final integration, conflict resolution, and verification decision.

## Owner bundle rules

- Assign each worker an explicit file list or component boundary.
- Keep shared contracts, public APIs, and cross-bundle naming decisions with the main agent unless delegated explicitly.
- Do not run concurrent edits against the same file or strongly coupled call chain.
- Require workers to report changed files, assumptions, verification, and open risks.
- Treat generated files, lock files, and broad formatting as shared ownership unless explicitly assigned.

## Good parallel tasks

- read-only architecture audit
- reference and call-chain discovery
- independent screen, adapter, or documentation bundle edits
- focused re-audit after integration

## Bad parallel tasks

- competing edits to a shared ViewModel, reducer, store, or DI composition root
- broad cleanup without ownership boundaries
- dependency upgrades while feature work is active
- formatting sweeps mixed with behavior changes

## Blocking criteria

A parallel wave is blocked when ownership overlaps, a shared contract must change, verification cannot be scoped, or workers report contradictory architecture assumptions. Stop, integrate findings, and re-plan before editing further.
