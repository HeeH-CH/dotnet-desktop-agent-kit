# Contributing

Thanks for your interest in contributing.

This project is focused on AI-agent guidance for .NET desktop application development.

## Good contributions

- WinUI/WPF-specific architecture rules
- MVVM and MVI-style state management guidance
- Clean Architecture for desktop application examples
- Roslyn MCP workflows for C# refactoring
- Microsoft Graph adapter boundary patterns
- CommunityToolkit.Mvvm usage examples
- Safer refactoring workflows for AI coding agents

## Out of scope

- Company-specific workflows
- Tenant-specific Microsoft 365 settings
- Real secrets, tokens, IDs, URLs, or internal system names
- General backend-only ASP.NET Core templates unless they support desktop integration
- Large framework debates without actionable guidance

## Contribution style

Prefer concise, practical guidance. Every new rule or skill should answer:

1. What problem does this prevent?
2. When should an agent use it?
3. What is the desired pattern?
4. What is the anti-pattern?
5. How can the agent verify the result?

## Keep related surfaces together

When a change affects an agent behavior, update the related surfaces in the same contribution where practical:

- Update `rules/` when the change introduces an always-on architectural constraint.
- Update `skills/` when the change describes a repeatable task an agent should invoke.
- Update `agents/` when a specialist agent must read a new rule, skill, or workflow before acting.
- Update `workflows/` when the change affects ordering, audit, delegation, runtime smoke, or verification.
- Update README files when the public shape of the kit changes.

Keep these surfaces aligned for Codex, Claude, rules, skills, workflows, specialist agents, and MCP/tool routing. Avoid documenting a behavior in only one place if another surface would lead an agent to a conflicting action.

## Generic guidance only

Do not include product-specific implementation details. Examples must be reusable across .NET desktop projects and must not mention private tenants, workspaces, customer names, internal URLs, secrets, production IDs, or company-specific process names.

## Pull request checklist

- [ ] The change is generic and safe to publish.
- [ ] No private/company/tenant-specific information is included.
- [ ] The change improves desktop .NET agent behavior.
- [ ] Related rules, skills, agents, or workflows were updated together.
- [ ] Codex, Claude, and MCP/tool routing guidance still point to the same behavior where relevant.
- [ ] Examples are small and reusable.
