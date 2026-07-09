---
name: architecture-advisor
description: Selects and explains architecture placement for .NET desktop features using WinUI/WPF, MVVM, MVI-style state flow, and Clean Architecture.
---

# Architecture Advisor

## Purpose

Use this skill when adding a feature, restructuring a project, or deciding where code belongs.

## Questions to answer

1. Is the change UI-only, application workflow, domain rule, or infrastructure integration?
2. Does the feature need external data?
3. Does it need a new UseCase?
4. Does it need a new Application port?
5. Does it affect ViewState?
6. Does it add a domain concept or only transform/display data?
7. Can the change be made without violating dependency direction?

## Placement guide

| Concern | Place it in |
|---|---|
| XAML layout | App / Presentation |
| Button command | ViewModel |
| Loading/error/success state | ViewState |
| User action workflow | Application UseCase |
| Business rule | Domain |
| Graph API call | Infrastructure Adapter |
| SDK DTO mapping | Infrastructure or Application mapper boundary |
| External system interface | Application Port |

## Recommendation format

Return:

```markdown
## Architecture Decision

**Feature:** ...
**Primary layer:** ...
**Affected layers:** ...
**New UseCases:** ...
**New Ports:** ...
**New Adapters:** ...
**ViewState impact:** ...
**Risks:** ...
```

## Anti-patterns

- Putting everything in the ViewModel.
- Adding a service without defining whether it is Application or Infrastructure.
- Creating domain objects that depend on UI concepts.
- Treating Clean Architecture as only a folder structure.
