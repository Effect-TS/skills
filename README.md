# Effect Skills

Agent skills for working effectively in repositories that use Effect.

This repository is designed to be installed by skill-aware coding agents so they can apply consistent Effect conventions, architecture guidance, and repo-backed best practices.

## Installation

```sh
npx skills add Effect-TS/skills
```

## Included Skills

### `effect-ts`

The main Effect skill provides guidance for:

- Effect usage and common constructors
- layers, services, and dependency injection
- schema design and transformations
- error handling
- SQL and migrations
- observability
- testing with `@effect/vitest`

It also expects a local vendored checkout of the Effect repo at `./.repos/effect` in the target project, and includes setup guidance for that workflow.

### `effect-v3-to-v4`

A bounded migration skill for upgrading a codebase from Effect v3 to Effect v4. It drives the migration from the generated `migration/v3-to-v4.md` reference in the Effect repo:

- shallow local checkouts of the v4 (`main`) and v3 branches
- search-only access to the migration reference (never read whole)
- an escalation chain from reference doc to topic guides to v4/v3 source
- repo-level guidance for package consolidation and version alignment

## Repository Layout

```text
skills/
  effect-ts/
    SKILL.md
    references/
      *.md
  effect-v3-to-v4/
    SKILL.md
```

Conventions:

- each skill lives at `skills/<skill-name>/SKILL.md`
- supporting guides and reference material live under `skills/<skill-name>/references/`

## Purpose

The goal of this repository is not just to expose API documentation. It is to encode strong implementation preferences for real Effect codebases, including:

- using local guides before source-level repo research
- preferring safe, typed, schema-driven code
- preferring `Effect.fn`, proper layers, and service encapsulation
- preferring Effect-native integrations such as Effect SQL and `@effect/vitest`

## Developing Skills

When adding a new skill:

1. create `skills/<skill-name>/SKILL.md`
2. add any detailed guides under `skills/<skill-name>/references/`
3. keep the skill operational and opinionated, not just descriptive
