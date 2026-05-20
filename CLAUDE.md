# @milkyskies/biome-config

Shared Biome config + GritQL plugins for milkyskies TypeScript projects. Published to npm. Consumed by milky-kit's TS templates.

Rules load from `.claude/rules/`, which holds symlinks into `~/.claude/kit/`. See milky-kit's README for the full set.

## Project-specific

- This repo is the source-of-truth for the `@milkyskies/biome-config` npm package. Bump version via release-please; never `pnpm version` by hand.
- The `no-as-cast.grit` GritQL plugin is declared in the shared `biome.json` as `./node_modules/@milkyskies/biome-config/plugins/no-as-cast.grit`. Biome resolves that from the consumer's `biome.json` location, so pnpm/bun pick it up automatically; plain-npm hoisting may not.
- Worktrees not wired up — the project is small enough for direct-on-main work.
