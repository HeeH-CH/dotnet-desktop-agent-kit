# Public Repository Safety

## Intent

Prevent private organizational information from entering a public agent kit.

## Applies to

Docs, examples, templates, issues, PRs, comments, and C# snippets.

## Rule

Use generic examples only. Never include real tenant IDs, client secrets, internal URLs, private project names, organization-specific workflow names, or personal information.

## Allowed

- `ExampleApp`, `ExampleGraphAdapter`, `YOUR_TENANT_ID`, `YOUR_CLIENT_ID`, `YOUR_REDIRECT_URI`.
- Generic M365 terms such as Calendar, Planner, To Do, User Profile.
- Example domains under `example.invalid`.

## Not allowed

- Real tenant IDs, client IDs, secrets, redirect URIs, or tokens.
- Company names or internal service names.
- Private repository names or internal URLs.
- Screenshots or logs with personal data.

## Preferred pattern

Replace real details with obvious placeholders and state users must provide their own local values.

## Anti-pattern

A Graph auth example that includes a real-looking GUID and organization-specific redirect URI.

## Agent verification

- Scan for secrets and private-looking identifiers.
- Check examples use generic namespaces.
- Check issue and PR templates include public-safety reminders.
