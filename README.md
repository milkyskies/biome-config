# @milkyskies/biome-config

Shared [Biome](https://biomejs.dev/) config + GritQL plugins for milkyskies TypeScript projects.

## What's in it

- `biome.json` — formatter (tab indent, double quotes, no semicolons, line width 100) + linter (recommended + `noExplicitAny: error`) + import organizer.
- `plugins/no-as-cast.grit` — bans `as` type assertions. Allowed: `as const`, `import { x as y }`, `import * as ns`. Suppress one-off legitimate cases with `// biome-ignore lint/plugin: <reason>`.

## Use it

Install from GitHub (no npm registry — git URL works with `bun`/`npm`/`pnpm`):

```bash
bun add -d github:milkyskies/biome-config @biomejs/biome
```

Add a project `biome.json` that extends the base AND wires in the plugin:

```json
{
	"$schema": "https://biomejs.dev/schemas/2.4.15/schema.json",
	"extends": ["@milkyskies/biome-config/biome.json"],
	"plugins": ["./node_modules/@milkyskies/biome-config/plugins/no-as-cast.grit"]
}
```

The `plugins` array can't live in the extended config — Biome resolves plugin paths relative to the file that declares them, and from the consumer's CWD the extended-side `./plugins/...` doesn't exist. Two lines of consumer boilerplate is the workaround.

Add scripts to your project `package.json`:

```json
{
	"scripts": {
		"check": "biome check --write",
		"format": "biome format --write",
		"lint": "biome lint"
	}
}
```

Agents writing code in projects that consume this config should run `bun run check` before claiming work done.

## Why a separate repo

Could live inside [milky-kit](https://github.com/milkyskies/milky-kit) as a module, but milky-kit's existing `ts-shared` module assumes a pnpm monorepo with `packages/biome-config` as a workspace. Standalone non-monorepo TS projects (matrix-windmill-gateway etc.) need this lighter sharing path. See [venus-desk#5](https://github.com/milkyskies/venus-desk/issues/5) for the long-term reconciliation question.
