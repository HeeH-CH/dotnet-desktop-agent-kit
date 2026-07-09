# Workflow: Verify Change

Use this after any meaningful change.

## Checks

1. Build
2. Tests, if available
3. Dependency direction
4. Code-behind responsibility check
5. ViewModel responsibility check
6. Infrastructure leakage check
7. Dead code or unused type check
8. Public API surface check when library projects changed

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
| Dead code | PASS/WARN/SKIP | |

## Verdict

READY / NEEDS FIXES
```
