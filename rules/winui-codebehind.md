# WinUI/WPF Code-Behind

## Intent

Keep code-behind limited to view-only behavior.

## Applies to

WinUI 3 and WPF pages, windows, user controls, and event handlers.

## Rule

Code-behind may initialize views, manage visual-tree-only concerns, or forward events to commands. Business decisions, IO, Graph calls, validation policy, and state transitions belong elsewhere.

## Allowed

- `InitializeComponent` and view-only setup.
- Focus, animation, or visual tree glue.
- Event handler that dispatches a ViewModel intent.

## Not allowed

- Microsoft Graph SDK calls from code-behind.
- File parsing, auth, persistence, or business branching in event handlers.
- Directly mutating controls after application operations.
- Creating Infrastructure adapters from a Page or Window.

## Preferred pattern

Move event behavior to a ViewModel intent. If it includes IO or branching, extract a UseCase.

## Anti-pattern

A button click handler authenticates, calls Graph, maps DTOs, and updates UI controls.

## Agent verification

- List changed code-behind files.
- Confirm handlers are view-only or intent dispatchers.
- Check for SDK, IO, HTTP, auth, and business branching.
