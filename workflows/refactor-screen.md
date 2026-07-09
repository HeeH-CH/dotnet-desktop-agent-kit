# Workflow: Refactor Screen

Use this when refactoring a WinUI/WPF screen.

## Steps

1. Inventory code-behind responsibilities.
2. Inventory ViewModel responsibilities.
3. Identify external SDK or Infrastructure leakage.
4. Identify UI states.
5. Extract commands or intent methods.
6. Extract UseCases for workflows.
7. Extract ports and adapters for external systems.
8. Replace scattered flags with ViewState.
9. Keep the app buildable after each step.
10. Document remaining debt.

## Final report

```markdown
## Screen Refactor Report

- Removed from code-behind:
- ViewModel changes:
- New/changed ViewState:
- New/changed UseCases:
- Adapter movement:
- Remaining debt:
```
