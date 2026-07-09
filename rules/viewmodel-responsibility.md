# ViewModel Responsibility

## Intent

Prevent ViewModels from becoming service containers while preserving MVVM ergonomics.

## Applies to

ViewModels, commands, observable properties, ViewState mapping, and injected dependencies.

## Rule

ViewModels own UI state, intent dispatching, presentation formatting, and UseCase coordination. They do not own SDK calls, persistence logic, or domain policy.

## Allowed

- Injecting focused UseCases.
- Mapping application Result to ViewState.
- Exposing commands and observable ViewState.

## Not allowed

- Injecting `GraphServiceClient` into a ViewModel.
- File IO, auth, retry, throttling, or persistence in commands.
- Raw adapter DTOs as observable properties.

## Preferred pattern

When a command grows beyond UI coordination, extract a UseCase.

## Anti-pattern

A ViewModel constructor with Graph, files, HTTP, cache, token, and storage services.

## Agent verification

- Classify injected dependencies.
- Check commands delegate application work to UseCases.
- Check no external SDK namespaces appear in ViewModels.
