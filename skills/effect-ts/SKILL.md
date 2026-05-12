---
name: effect-ts
description: Use this skill whenever working in a repository that uses Effect, even if the current task is in a new file or the user does not explicitly ask for Effect help. Apply it to any work that should follow the repository's Effect patterns, conventions, architecture, or supporting tooling. Also use it for questions about Effect patterns, services, layers, schemas, streams, runtimes, or typed error handling.
---

# Effect Expert

Expert guidance for programming with the Effect library, covering error handling, dependency injection, composability, and testing patterns.

## Prerequisite

Before doing any other Effect-related work, check that `./.repos/effect` exists at the root of the repository where the skill is being used.

If it does not exist, stop and prompt the user with the setup task documented in `./references/setup.md`.

## Research Strategy

Effect has many ways to accomplish the same task. Proactively research best practices when working with Effect patterns, especially for moderate to high complexity tasks.

### Research Sources

1. Codebase patterns first. Examine similar patterns in the current project before implementing. If Effect patterns already exist, follow them for consistency. If no patterns exist, skip this step.
2. Effect source code. For complex type errors, unclear behavior, or implementation details, examine the vendored Effect source at `./.repos/effect/packages/effect/src/`.

### When To Research

- Always research for services, layers, or complex dependency injection.
- Always research for error handling with multiple error types or complex error hierarchies.
- Always research for stream-based operations and reactive patterns.
- Always research for resource management with scoped effects and cleanup.
- Always research for concurrent or performance-critical code.
- Always research for unfamiliar testing patterns.
- Research when needed for complex refactors from promises or try/catch into Effect.
- Research when needed for new service dependencies or layer restructuring.
- Research when needed for custom error types or extensions of existing error hierarchies.
- Research when needed for integrations with external systems such as databases, APIs, or third-party services.

### Research Approach

- Focus on canonical, readable, and maintainable solutions rather than clever optimizations.
- Verify suggested approaches against existing codebase patterns when those patterns exist.
- When multiple approaches are possible, prefer the most idiomatic Effect solution supported by the codebase and the vendored source.

### Codebase Pattern Discovery

When working in a project that uses Effect, check for existing patterns before implementing new code:

1. Search for Effect imports and existing module usage to understand current conventions.
2. Identify how services and layers are structured in the project.
3. Note how errors are defined and propagated.
4. Examine how Effect code is tested in the project.

If no Effect patterns exist in the codebase, proceed using canonical patterns from the vendored Effect source and examples. Do not block on missing codebase patterns.

### Feature Discovery

When you need to discover available Effect modules, packages, or capabilities, search `./references/features.md` first.

- Use it to identify the right package or module for a task.
- Use the listed repo paths to jump directly into the vendored source under `./.repos/effect`.
- Use it before inventing custom abstractions when Effect may already provide the functionality.

### Guide Discovery

When the task touches one of these areas, consult the matching guide before implementing:

- `./references/guide-error-handling.md` for defining errors, schema-based errors, failure handling, defects, and interrupts
- `./references/guide-layers.md` for services, layer construction, composition, and provisioning patterns
- `./references/guide-observability.md` for `Effect.fn`, spans, logging, metrics, and telemetry wiring

## Effect Principles

Apply these core principles when writing Effect code.

### Error Handling

- Use Effect's typed error system instead of throwing exceptions.
- Define descriptive error types with proper error propagation.
- Use `Effect.fail`, `Effect.catchTag`, and `Effect.catch` for error control flow.

### Dependency Injection

- Implement dependency injection using services and layers.
- Define services with `Context.Tag`.
- Compose layers with `Layer.merge` and `Layer.provide`.
- Use `Effect.provide` to inject dependencies at the edge, avoid providing locally.

### Composability

- Leverage Effect composability for complex operations.
- Use appropriate constructors such as `Effect.succeed`, `Effect.fail`, `Effect.tryPromise`, `Effect.try`, and `Effect.sync`.
- Apply proper resource management with scoped effects.
- Chain operations with `Effect.flatMap`, `Effect.map`, and `Effect.tap`.

### Code Quality

- Write type-safe code that leverages Effect's type system.
- Use `Effect.gen` for readable sequential code.
- Implement proper testing patterns using Effect testing utilities.
- Prefer existing Effect primitives before introducing custom helpers.

### Explaining Solutions

When providing solutions, explain the Effect concepts being used and why they fit the specific use case. If you encounter patterns not covered in local references, prefer consistency with the codebase when possible and otherwise rely on the vendored Effect source.

## References

- `./references/features.md`
- `./references/guide-error-handling.md`
- `./references/guide-layers.md`
- `./references/guide-observability.md`
- `./references/setup.md`
