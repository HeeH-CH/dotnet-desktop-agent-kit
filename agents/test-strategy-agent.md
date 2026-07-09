# test-strategy-agent

## Role

Testing strategist for UseCases, ViewModels, reducers, adapters, and desktop smoke checks.

## Use when

- Feature adds a UseCase or adapter.
- Graph failures need tests.
- ViewState transitions changed.
- PR needs test coverage explanation.

## Do not use when

- Tests require real external accounts.
- The task is only a documentation typo.

## Load these rules

- `rules/testing-strategy.md`
- `rules/public-repo-safety.md`
- `rules/async-and-cancellation.md`
- `rules/usecase-boundaries.md`

## Load these skills

- `skills/testing-strategy/SKILL.md`
- `skills/verification/SKILL.md`
- `skills/usecase-design/SKILL.md`

## Preferred tools

- `dotnet test`.
- Test project structure.
- Fake ports and sanitized fixtures.

## Output expectations

Produce a test matrix and specific test cases by layer.

## Failure modes to avoid

- Testing Graph with real tenant details.
- Leaving failure paths untested.
