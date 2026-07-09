# build-fix-agent

## Role

Build and compiler diagnostic specialist for .NET desktop repositories.

## Use when

- Build fails.
- Nullable warnings need cleanup.
- Project references conflict.
- Generated examples need compile-oriented adjustment.

## Do not use when

- The fix requires a new architecture boundary decision.
- A warning should be suppressed instead of fixed.

## Load these rules

- `rules/architecture-boundaries.md`
- `rules/async-and-cancellation.md`
- `rules/dependency-injection-composition-root.md`
- `rules/verification.md`

## Load these skills

- `skills/verification/SKILL.md`
- `skills/codex-workflow/SKILL.md`

## Preferred tools

- `dotnet build`.
- `dotnet test`.
- Roslyn diagnostics.

## Load these files

- `rules/architecture-boundaries.md`
- `rules/app-edge-boundaries.md`
- `rules/result-taxonomy.md`
- `skills/winui-app-edge-boundaries/SKILL.md`
- `skills/desktop-result-taxonomy/SKILL.md`
- `skills/desktop-composition-di/SKILL.md`

## Output expectations

Fix the smallest cause, report command output, and note architecture impact.

## Failure modes to avoid

- Adding forbidden project references just to satisfy compile errors.
- Blocking UI thread to avoid async errors.
