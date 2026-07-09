# Workflow: Parallel Wave

Use this for broad refactoring, multi-area feature work, or architecture audits where separate workers can help without overlapping ownership.

## Steps

1. Define the goal, non-goals, allowed files, forbidden files, and verification limit.
2. Split owner bundles by file list, component, or layer boundary.
3. Run read-only discovery or audit before implementation when requirements are broad or risky.
4. Integrate findings into one plan.
5. Assign scoped implementation bundles only when ownership is disjoint.
6. Re-audit the changed bundles against the original plan and rules.
7. Fix blocking findings, then re-audit narrowly.
8. Run the narrowest meaningful verification.
9. Report changed files, design summary, verification, and remaining risks.

## Read-only audit prompt

```text
You are auditing only. Do not edit files.

Goal:
Allowed files:
Forbidden files:
Rules to check:
- rules/app-edge-boundaries.md
- rules/result-taxonomy.md
- rules/parallel-wave.md
- rules/error-learning.md

Report:
- Findings ordered by severity with file references
- Boundary or ownership risks
- Missing verification
- No implementation plan unless a finding requires it
```

## Implementation worker prompt

```text
You own only this bundle:

Allowed files:
Forbidden files:
Goal:
Architecture constraints:
Verification limit:

Before editing, read the relevant rules and existing local patterns.
Keep edits scoped to your bundle.
Do not change shared contracts unless explicitly assigned.

Report:
- Files changed
- Design summary
- Verification performed
- Risks or handoff notes
```

## Re-audit prompt

```text
You are re-auditing completed changes. Do not edit files.

Original goal:
Changed files:
Rules to check:
Verification performed:

Report only blocking or material findings:
- Requirement gaps
- Ownership violations
- App-edge boundary leaks
- Result taxonomy violations
- Missing or misleading verification
```

## Owner bundle rules

- One owner per file during implementation.
- One owner per tightly coupled reducer/store/ViewModel bundle.
- The main agent owns integration, shared contracts, public API naming, and final verification.
- Workers may inspect outside their bundle but must not edit outside it.
- If a required change crosses ownership, stop and report the handoff instead of editing.

## Blocking criteria

- Allowed or forbidden file boundary is violated.
- Raw App-edge authority moves inward.
- User-visible failures remain `bool`, raw exception, or `exception.Message` where typed results are required.
- Two workers need the same file or shared contract.
- Verification claims do not match commands that were actually run.

## Final report

```markdown
## Parallel Wave Report

- Owner bundles:
- Files changed:
- Blocking findings resolved:
- Verification:
- Remaining risks:
```
