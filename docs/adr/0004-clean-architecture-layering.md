# ADR: Clean Architecture Layering

## Status

Accepted

## Context

Desktop apps need boundaries around UI, use cases, domain concepts, and external integrations.

## Decision

Use App/Presentation, Application, Domain, and Infrastructure as conceptual layers. Enforce dependency direction and responsibility rules.

## Consequences

Graph, file, auth, and local storage details stay out of ViewModels and Domain.
