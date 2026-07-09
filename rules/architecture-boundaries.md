# Architecture Boundaries

## Intent

Prevent Clean Architecture from becoming folder naming only.

## Applies to

Projects, namespaces, references, public contracts, examples, and refactors.

## Rule

Keep dependency direction inward: `App -> Application -> Domain`, `Infrastructure -> Application / Domain`, and `Domain -> no external dependencies`.

## Allowed

- ViewModel calls an Application UseCase.
- Infrastructure implements an Application port.
- Application DTOs expose app-level data, not SDK DTOs.
- Domain contains framework-independent business concepts.

## Not allowed

- Application references WinUI/WPF types.
- Domain references Infrastructure, Graph SDK, HTTP clients, or DI containers.
- ViewModel constructs SDK clients or adapters directly.
- Clean Architecture is treated as folder naming only.

## Preferred pattern

Classify each changed type by layer before editing. Split mixed types into Presentation state, Application flow, Domain concept, and Infrastructure adapter.

## Anti-pattern

Moving files into folders named Application and Domain while preserving the original UI/SDK dependencies.

## Agent verification

- Inspect project references or Roslyn project graph.
- Search for UI namespaces in Application/Domain.
- Search for Infrastructure references from Domain.
- Check ViewModels for SDK clients or adapters.
