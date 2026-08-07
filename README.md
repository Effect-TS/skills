# Effect Skills

Agent skills for working effectively in repositories that use Effect.

This repository is designed to be installed by skill-aware coding agents so they can apply consistent Effect conventions, architecture guidance, and repo-backed best practices.

## Installation

```sh
npx skills add Effect-TS/skills
```

## Included Skills

### `effect-ts`

The main Effect skill directs agents to the guidance shipped with the installed Effect package at `node_modules/effect/AGENTS.md`.

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
  effect-v3-to-v4/
    SKILL.md
```

Conventions:

- each skill lives at `skills/<skill-name>/SKILL.md`
- skills can include supporting files when needed

## Purpose

The main skill keeps guidance aligned with the installed Effect version by relying on the package's own `AGENTS.md`. The migration skill provides a focused workflow for v3-to-v4 upgrades.

## Developing Skills

When adding a new skill:

1. create `skills/<skill-name>/SKILL.md`
2. add supporting files only when the skill needs them
3. keep the skill operational and concise
