# Contributing

Thanks for helping improve .NET Desktop Agent Kit.

This repository is for public, generic AI-agent guidance for .NET desktop application development. It is not a place for company-specific prompts or private implementation notes.

## Good contributions

- WinUI/WPF-specific architecture rules.
- MVVM and MVI-style state management guidance.
- Clean Architecture examples for desktop apps.
- Roslyn MCP workflows for C# refactoring.
- Microsoft Graph/M365 adapter boundary patterns.
- CommunityToolkit.Mvvm usage guidance.
- Safer refactoring workflows for AI coding agents.

## Out of scope

- Company-specific workflows.
- Tenant-specific Microsoft 365 settings.
- Real secrets, tokens, IDs, URLs, or internal system names.
- Backend-only ASP.NET Core templates unless clearly connected to desktop integration.

## Contribution style

Every new rule or skill should answer: what problem this prevents, when an agent should use it, desired pattern, anti-pattern, and verification.

Use small examples with generic namespaces such as `ExampleApp.Application.Calendar`, `ExampleApp.Infrastructure.Graph`, and `ExampleApp.App.ViewModels`.

## Pull request checklist

- [ ] The change is generic and safe to publish.
- [ ] No private/company/tenant-specific information is included.
- [ ] The change improves desktop .NET agent behavior.
- [ ] Related rules, skills, agents, workflows, or docs were updated together.
- [ ] Examples are small and reusable.
- [ ] Links were checked where possible.
