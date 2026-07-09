# Verification Rule

## Intent

Every meaningful agent change should leave the project easier to trust.

## Required report

After a feature, refactor, or fix, report:

- build status
- changed files
- architecture boundary impact
- ViewModel responsibility changes
- UseCase changes
- adapter changes
- known risks
- follow-up recommendations

## Preferred checks

- `dotnet build`
- `dotnet test` when tests exist
- Roslyn diagnostics when available
- project dependency graph
- circular dependency detection
- dead code detection

## Refactoring safety

Prefer small, reversible steps. A refactoring step is good when:

- the project still builds
- behavior is intentionally preserved
- responsibility moved in one direction only
- names became clearer
- no new external dependency leaked inward
