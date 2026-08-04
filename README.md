# Effect Skills

Agent skills for working effectively in repositories that use Effect.

This repository is designed to be installed by skill-aware coding agents so they can apply consistent Effect conventions, architecture guidance, and repo-backed best practices.

## Installation

Two routes, reading the same skill files.

**As loose skills**, via [skills.sh](https://skills.sh) — copies editable skill files into your project, unnamespaced:

```sh
npx skills add Effect-TS/skills                    # all of them
npx skills add Effect-TS/skills --skill effect-ts  # just one
```

**As a Claude Code plugin** — read-only, always current, and namespaced so it cannot collide with a skill of the same name elsewhere:

```text
/plugin marketplace add Effect-TS/skills
/plugin install effect-skills@effect-ts
```

## Invoking a Skill

Skills fire two ways: automatically, when what you ask matches the skill's `description`; or by name, typed as a slash command. Installed as a plugin the name is namespaced — `/effect-skills:effect-ts` rather than `/effect-ts`.

`effect-v3-to-v4` sets `disable-model-invocation: true`, so it never fires automatically — invoke it by name when you are ready to migrate.

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
.claude-plugin/
  plugin.json       # Claude Code plugin manifest; lists each skill path
  marketplace.json  # marketplace manifest, so the repo installs as a marketplace
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
3. register the skill path in `.claude-plugin/plugin.json` so plugin users get it too
4. keep the skill operational and opinionated, not just descriptive
