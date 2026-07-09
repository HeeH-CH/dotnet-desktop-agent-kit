# WinUI/WPF Code-behind Rule

## Intent

Keep code-behind thin and view-only.

## Allowed in code-behind

- UI initialization
- view-only event bridging when binding is not practical
- visual tree concerns
- focus management
- window sizing and positioning
- platform UI interop that cannot be expressed in XAML or ViewModel

## Not allowed in code-behind

- business rules
- API calls
- persistence logic
- Microsoft Graph calls
- feature orchestration
- domain decisions
- long-running workflows

## Preferred pattern

Move user actions into ViewModel commands or intent methods.

```text
Button click -> Command -> Intent -> UseCase -> ViewState update
```

## Agent verification

Before editing code-behind, ask whether the logic belongs in:

- ViewModel
- UseCase
- Domain model
- Infrastructure adapter

Only keep code in code-behind when it is truly view-specific.
