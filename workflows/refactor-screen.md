# Workflow: Refactor Screen

Use this when refactoring a WinUI/WPF screen.

Read the relevant rules first:

- `rules/winui-codebehind.md`
- `rules/app-edge-boundaries.md`
- `rules/mvi-state-flow.md`
- `rules/result-taxonomy.md`

## Steps

1. Inventory code-behind responsibilities.
2. Inventory ViewModel responsibilities.
3. Identify external SDK or Infrastructure leakage.
4. Identify App-edge authority that must remain at the View/App host boundary.
5. Identify UI states.
6. Define result taxonomy for user-visible actions that can fail.
7. Extract commands or intent methods.
8. Extract UseCases for workflows.
9. Extract ports and adapters for external systems.
10. Replace scattered flags with ViewState.
11. Keep the app buildable after each step.
12. Document remaining debt.

## Final report

```markdown
## Screen Refactor Report

- Removed from code-behind:
- App-edge authority kept at boundary:
- ViewModel changes:
- New/changed ViewState:
- Result taxonomy:
- New/changed UseCases:
- Adapter movement:
- Remaining debt:
```
