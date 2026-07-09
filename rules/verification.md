# Verification

## Intent

Make every agent change auditable and prevent silent architecture regression.

## Applies to

Code, docs, rules, skills, workflows, templates, and PRs.

## Rule

Every meaningful change must report what was verified, what was not verified, and why.

## Allowed

- `dotnet build` and `dotnet test` results.
- Roslyn MCP project graph, diagnostics, references, and implementation checks.
- Markdown link checks for docs changes.
- Public-safety review for examples and templates.

## Not allowed

- Saying “looks good” without checks.
- Hiding unavailable tooling.
- Claiming tests passed when they were not run.

## Preferred pattern

Use a verification table with Check, Result, and Notes. Mark unavailable tools explicitly.

## Anti-pattern

Final report lists changed files but omits build, tests, architecture, and safety checks.

## Agent verification

- Ensure final report contains the required table.
- Check each not-run item has a reason.
- Confirm known risks are listed.
