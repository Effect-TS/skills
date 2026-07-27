---
name: effect-v3-to-v4
description: Use this skill when migrating a codebase from Effect v3 to Effect v4 (the 4.0.0-beta line), when upgrading `effect` or `@effect/*` packages across the v3/v4 boundary, or when a v3 API is missing, renamed, or behaves differently in v4. Also use it when diagnosing post-upgrade type errors such as "Property does not exist on type" or unresolved imports from `effect` or `@effect/*`.
---

# Effect v3 → v4 Migration

Migrate code from Effect v3 to Effect v4 using the migration guides that ship with the Effect source, and the v4 source itself as the final authority.

Never guess at a v4 replacement. Every replacement API must be traced to either a migration guide or the v4 source.

## Prerequisite: Local Effect Checkout

This skill requires a local checkout of the Effect repository at `./.repos/effect` in the repository being migrated. The migration guides and the v4 source both live there.

If `./.repos/effect` does not exist, clone it before doing anything else:

```sh
mkdir -p .repos
git clone --depth 1 https://github.com/Effect-TS/effect .repos/effect
```

Notes:

- clone the `main` branch — that is the v4 line
- add `.repos/effect` to `.gitignore` unless the host repository already vendors it as a subtree or submodule
- if the checkout already exists but is old, `git -C .repos/effect pull` before relying on it — v4 is in beta and the guides change between beta releases

## Reference Documents

The v3 → v4 reference doc is `./.repos/effect/MIGRATION.md`. Read it first. It covers:

- single shared version number across all Effect packages
- package consolidation — `@effect/platform`, `@effect/rpc`, `@effect/cluster` and others moved into `effect`
- the `effect/unstable/*` module system
- an index linking to per-topic guides in `./.repos/effect/migration/`

The per-topic guides in `./.repos/effect/migration/` are the detailed source of replacements. Read the ones relevant to the code being migrated. Treat the index in `MIGRATION.md` as authoritative for what exists — do not assume a guide is missing because you did not find it, and do not assume one exists because a topic feels like it should have one.

## Workflow

1. **Inventory.** List the Effect APIs the target code actually uses — imports from `effect` and every `@effect/*` package, plus the combinators called on them. Scope the migration to what is in use.
2. **Read the index.** Read `./.repos/effect/MIGRATION.md`, then read every guide in `./.repos/effect/migration/` that matches the inventory.
3. **Align versions.** Bring `effect` and all `@effect/*` packages onto matching v4 beta versions. Drop packages that were consolidated into `effect` and re-point their imports.
4. **Apply guided replacements.** For each API covered by a guide, apply the documented replacement. Prefer the guide's shape over a mechanical rename — several v4 changes are structural, not textual.
5. **Resolve the gaps.** For an API the guides do not mention, search the v4 source before concluding anything (see below).
6. **Verify.** Type-check and run the test suite. A migration is not done until the code compiles against v4 and tests pass. Report any API you could not resolve rather than leaving a silent workaround.

## Resolving APIs Not Covered by a Guide

When a v3 API is missing or changed and no migration guide covers it, search `./.repos/effect` in this order:

1. `./.repos/effect/packages/effect/src/` — the core v4 source, including `unstable/` for modules that have not stabilized yet
2. the relevant package under `./.repos/effect/packages/` for platform, SQL, AI, and OpenTelemetry APIs
3. `./.repos/effect/.changeset/` — pending changesets often describe a rename or new API before it reaches a guide

Search by symbol name and by behaviour, since many v4 changes are renames. Confirm the replacement's real signature by reading its definition in the source, not by inferring it from a call site.

If an API has no v4 equivalent, say so explicitly and propose an implementation built from existing v4 primitives. Do not reintroduce a v3-shaped helper to paper over the gap.

## Constraints

- Do not invent APIs. If it is not in a guide or the v4 source, it does not exist.
- Do not use `any` or `as` casts to silence a v4 type error. A type error after migration usually means the replacement API has a different shape — go back to the source.
- Do not mix v3 and v4 packages in one project. All `effect` and `@effect/*` versions must be aligned.
- Prefer stable `effect/*` imports; use `effect/unstable/*` only when the module has not graduated, and note that unstable modules can break in minor releases.
- Migrate incrementally — one module or package at a time, type-checking between steps — rather than rewriting everything before the first compile.

## Related Skills

For writing idiomatic v4 code once the migration is done, use the `effect-ts` skill.
