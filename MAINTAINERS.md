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

- `drywintun-<upstream-version>-x64.zip`
- `drywintun-<upstream-version>-arm64.zip`
- `drywintun-<upstream-version>-x86.zip`
- `wintun-<upstream-version>.zip` (fetched from wintun.net)

## Runner requirements

The workflows run on GitHub-hosted `windows-2022` runners.
