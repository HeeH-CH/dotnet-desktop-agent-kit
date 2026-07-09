# OpenCode Agent Guide

Use the root `AGENTS.md` as the source of truth. This entrypoint mirrors the desktop-first routing used by Codex CLI and Claude Code.

## Defaults

- Keep WinUI/WPF views thin.
- Put user actions through ViewModel intents.
- Move application flow into UseCases.
- Keep Graph, auth, files, local storage, and external APIs behind Infrastructure adapters.
- Prefer Roslyn MCP semantic analysis when available.
- Keep examples generic and public-safe.
