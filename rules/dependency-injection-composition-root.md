# Dependency Injection Composition Root

## Intent

Keep dependency wiring explicit without leaking Infrastructure into Domain or ViewModels.

## Applies to

App startup, host builders, service registration modules, navigation, and window creation.

## Rule

Composition root may reference all layers to wire dependencies. That exception does not permit ViewModels or UseCases to depend on Infrastructure implementations directly.

## Allowed

- App startup registers UseCases and Infrastructure adapters.
- Infrastructure extension method binds ports to adapters.
- ViewModel receives UseCases through constructor injection.

## Not allowed

- Domain project references a DI container.
- UseCase calls a service provider to resolve adapters.
- ViewModel uses a global service locator.

## Preferred pattern

Use small registration methods such as `AddApplication()` and `AddInfrastructure()` from the App composition root.

## Anti-pattern

A static service locator accessible from every layer.

## Agent verification

- Inspect project references around startup.
- Check service provider usage outside composition root.
- Confirm port-to-adapter bindings happen in the composition root.
