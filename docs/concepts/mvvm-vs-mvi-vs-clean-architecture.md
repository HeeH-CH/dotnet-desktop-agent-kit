# MVVM vs MVI vs Clean Architecture

MVVM, MVI, and Clean Architecture operate at different levels. They can be combined in a .NET desktop app.

## MVVM

MVVM is a Presentation-layer pattern commonly used by WPF and WinUI apps. The View owns XAML and visual behavior. The ViewModel owns bindable state, commands, and user intent dispatch.

## MVI-style state flow

MVI-style flow makes UI state transitions explicit. In this kit, it does not replace MVVM. A ViewModel command behaves like an intent, an Application UseCase returns Result, and the ViewModel reduces Result into ViewState.

```text
Intent -> UseCase -> Result -> Reducer -> ViewState
```

## Clean Architecture

Clean Architecture is an application-wide dependency and responsibility boundary pattern.

```text
App -> Application -> Domain
Infrastructure -> Application / Domain
Domain -> no external dependencies
```

It is not a folder naming convention.

## How they fit together

MVVM/MVI are UI Presentation-layer patterns. Clean Architecture is an application-wide dependency/responsibility boundary pattern. VSA, DDD, Modular Monolith, and similar approaches are different architectural choices at other levels. Therefore MVVM + MVI-style state flow + Clean Architecture can be used together without conflict.

## Desktop example

A Calendar screen can use `CalendarView.xaml`, `CalendarViewModel`, `CalendarViewState`, `LoadCalendarEventsUseCase`, `ICalendarGateway`, and `GraphCalendarGateway`. The ViewModel never calls Graph directly, the UseCase never references WinUI/WPF, and the adapter never exposes Graph SDK DTOs to ViewState.
