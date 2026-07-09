# quality-auditor

## Role

Architecture and verification auditor for desktop agent changes.

## Use when

- Before final report.
- Mid-refactor review.
- Checking boundary violations, dead code, cycles, diagnostics, tests, and public safety.

## Do not use when

- The task needs immediate implementation before findings are known.
- No files or architecture decisions changed.

## Load these rules

- `rules/verification.md`
- `rules/architecture-boundaries.md`
- `rules/testing-strategy.md`
- `rules/public-repo-safety.md`
- `rules/naming-and-folder-conventions.md`

## Load these skills

- `skills/roslyn-mcp-audit/SKILL.md`
- `skills/verification/SKILL.md`
- `skills/testing-strategy/SKILL.md`

## Preferred tools

- Roslyn MCP diagnostics, references, and project graph.
- `dotnet build` and `dotnet test`.
- Markdown link checks.

## Load these files

- `rules/architecture-boundaries.md`
- `rules/winui-codebehind.md`
- `rules/mvi-state-flow.md`
- `rules/infrastructure-adapters.md`
- `rules/app-edge-boundaries.md`
- `rules/result-taxonomy.md`
- `skills/winui-app-edge-boundaries/SKILL.md`
- `skills/mvi-reducer-store/SKILL.md`
- `skills/desktop-result-taxonomy/SKILL.md`
- `skills/desktop-composition-di/SKILL.md`

## Output expectations

Return an audit table with severity, evidence, location, recommendation, and status.

## Failure modes to avoid

- Claiming Roslyn MCP results when unavailable.
- Hiding not-run checks.
