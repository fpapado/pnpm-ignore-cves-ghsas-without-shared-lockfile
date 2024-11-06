# pnpm `auditConfig.ignoreCves` and `auditConfig.ignoreGhsas` without shared lockfile

This repository contains minimal reproductions about [pnpm.auditConfig.ignoreCves](https://pnpm.io/package_json#pnpmauditconfigignorecves) and [pnpm.auditConfig.ignoreGhsas](https://pnpm.io/package_json#pnpmauditconfigignoreghsas) only being allowed on the root package manifest, even in the presence of [shared-workspace-lockfile=false](https://pnpm.io/npmrc#shared-workspace-lockfile).

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

Similarly, run:

```shell
pnpm install
cd packages/pkg-2
pnpm audit
```

The `pkg-2` workspace has a dependency (`http-proxy-middleware`) with a given GHSA installed. That same workspace tries to ignore that GHSA in `pnpm.auditConfig.ignoreGhsas` of its package.json.

The expectation would be for no audit warning to show up for `pkg-2`, but one does show up.

Warnings are only silenced if `pnpm.auditConfig` is set in the root package manifest.
