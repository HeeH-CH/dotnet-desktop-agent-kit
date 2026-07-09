# .NET Desktop Agent Kit Cursor Rule

When editing WinUI/WPF desktop apps, follow the root `AGENTS.md` doctrine from this kit.

- No business logic in code-behind.
- No Microsoft Graph SDK calls from ViewModels.
- No WinUI/WPF references from Application or Domain.
- External SDK DTOs must not be exposed in ViewState.
- Use View -> Intent -> ViewModel -> UseCase -> Port -> Adapter -> Result -> ViewState -> View.
- Prefer Roslyn MCP or compiler-backed semantic checks before broad refactors.
- Keep examples generic and public-safe.
