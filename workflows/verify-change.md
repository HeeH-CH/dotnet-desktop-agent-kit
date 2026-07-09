# Workflow: Verify Change

Use this after any meaningful change.

Read the relevant rules first:

- `rules/verification.md`
- `rules/app-edge-boundaries.md`
- `rules/result-taxonomy.md`
- `rules/error-learning.md`

## Checks

1. Build
2. Tests, if available
3. Dependency direction
4. Code-behind responsibility check
5. ViewModel responsibility check
6. Infrastructure leakage check
7. App-edge authority check
8. Result taxonomy check for user-visible actions
9. Dead code or unused type check
10. Public API surface check when library projects changed
11. Runtime smoke when interactive confidence is required

## Final report

```markdown
## Verification Report

| Check | Result | Notes |
|---|---|---|
| Build | PASS/FAIL/SKIP | |
| Tests | PASS/FAIL/SKIP | |
| Dependency direction | PASS/FAIL | |
| Code-behind | PASS/WARN/FAIL | |
| ViewModel responsibilities | PASS/WARN/FAIL | |
| Infrastructure leakage | PASS/WARN/FAIL | |
| App-edge authority | PASS/WARN/FAIL/SKIP | |
| Result taxonomy | PASS/WARN/FAIL/SKIP | |
| Dead code | PASS/WARN/SKIP | |
| Runtime smoke | PASS/FAIL/SKIP | |

## Verdict

READY / NEEDS FIXES
```
