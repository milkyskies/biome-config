# @milkyskies/biome-config

Shared Biome config + GritQL plugins for milkyskies TypeScript projects. Published to npm. Consumed by milky-kit's TS templates.

## Rules

@~/.claude/kit/modules/core/rules/general.md
@~/.claude/kit/modules/core/rules/comments.md
@~/.claude/kit/modules/core/rules/config-and-env.md
@~/.claude/kit/modules/core/rules/workflow.md
@~/.claude/kit/modules/core/rules/worktrees.md

@~/.claude/kit/modules/security/rules/security.md
@~/.claude/kit/modules/release-please/rules/release-please.md

## Project-specific

- This repo is the source-of-truth for the `@milkyskies/biome-config` npm package. Bump version via release-please; never `pnpm version` by hand.
- The `no-as-cast.grit` GritQL plugin is declared as `./node_modules/@milkyskies/biome-config/plugins/no-as-cast.grit` in the shared `biome.json`. Biome resolves this from the CONSUMER'S biome.json location — so pnpm/bun setups pick it up automatically; plain-npm hoisting may break.
- No CI job here (no tests, no typecheck — the package is two files of config). Validation happens at consumer projects when they run biome against their code.
- Worktree mise tasks are not wired up for this repo; the project is small enough to work on directly on main.
