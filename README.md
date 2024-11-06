# `pnpm` `ignoreCves` and `ignoerGhsas` with `shared-workspace-lockfile=false`

This repository contains minimal reproductions about [pnpm.auditConfig.ignoreCves] and [pnpm.auditConfig.ignoreGhsas] only being allowed on the root package manifest, even in the presence of [shared-works-pace-lockfile=false](https://pnpm.io/npmrc#shared-workspace-lockfile)

## How to use

You will need node and pnpm.

Run:

```shell
pnpm install
pnpm audit
```

The expectation would be for no warnings to show up in `pkg-2`, but one does show up.
