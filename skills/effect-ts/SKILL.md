---
name: effect-ts
description: Use this skill whenever working in a repository that uses Effect, even if the current task is in a new file or the user does not explicitly ask for Effect help. Apply it to any work that should follow the repository's Effect patterns, conventions, architecture, or supporting tooling. Also use it for questions about Effect patterns, services, layers, schemas, streams, runtimes, or typed error handling.
---

# Effect Expert

Expert guidance for programming with the Effect library, covering error handling, dependency injection, composability, and testing patterns.

## Prerequisite

Before doing any other Effect-related work, check that `./.repos/effect` exists at the root of the repository where the skill is being used.

If it does not exist, stop and prompt the user with the setup task documented in `./references/setup.md`.

## Goals

- Prefer straightforward Effect composition over ad hoc async code.
- Keep layers, services, and error channels explicit.
- Preserve type safety while keeping implementations small.

## Working Style

- Reach for existing Effect primitives before introducing custom helpers.
- Keep effects local and composable.
- Model expected failures in the error channel instead of throwing.

## References

- `./references/setup.md`
