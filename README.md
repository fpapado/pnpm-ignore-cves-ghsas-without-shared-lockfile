# `pnpm` `ignoreCves` and `ignoreGhsas` with `shared-workspace-lockfile=false`

This repository contains minimal reproductions about [pnpm.auditConfig.ignoreCves] and [pnpm.auditConfig.ignoreGhsas] only being allowed on the root package manifest, even in the presence of [shared-works-pace-lockfile=false](https://pnpm.io/npmrc#shared-workspace-lockfile)

## How to use

You will need node and pnpm.

Run:

```shell
pnpm install
cd packages/pkg-1
pnpm audit
```

The `pkg-1` workspace has a dependency (`cookie`) with a given CVE installed. That same workspace tries to ignore that CVE in `pnpm.auditConfig.ignoreCves` of its package.json.

The expectation would be for no audit warning to show up for `pkg-1`, but one does show up.

Warnings are only silenced if `pnpm.auditConfig` is set in the root package manifest.
