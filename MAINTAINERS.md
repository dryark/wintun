# Dry Ark Wintun Mirror

This repository mirrors official Wintun source and publishes reproducible release assets for downstream projects.

## Source of truth

- Upstream source: `https://github.com/WireGuard/wintun`
- Mirror target: `https://github.com/dryark/wintun`

## Maintainer workflow

1. Sync from upstream:
   - `git fetch upstream`
   - `git checkout master`
   - `git merge --ff-only upstream/master`
2. Push updated source to origin (`dryark/wintun`).
3. Tag a release commit (for example `v0.14.1-dryark.1`) and push the tag.
4. Let `.github/workflows/release.yml` build and publish assets.
5. Update downstream consumers (for example `py-tuntap-abi3`) with the new tag and SHA256 values.

## Release assets produced

- `drywintun-amd64.dll`
- `drywintun-arm64.dll`
- `drywintun-x86.dll`
- `wintun-<upstream-version>.zip` (fetched from wintun.net)
- `UPSTREAM_SYS_STATUS.txt`
- `*.sys` files extracted from upstream package, when present
- `SHA256SUMS.txt`

## Runner requirements

The workflows run on GitHub-hosted `windows-2022` runners.
