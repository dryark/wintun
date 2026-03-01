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

- `wintun-amd64.dll`
- `wintun-arm64.dll`
- `wintun-x86.dll`
- `SHA256SUMS.txt`

## Runner requirements

The workflows are configured for a self-hosted Windows runner with Visual Studio Build Tools and WDK installed.
