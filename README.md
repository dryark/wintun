# Dry Ark Wintun Fork

This repository is a fork/mirror of upstream Wintun focused on reproducible userspace builds and downstream packaging for `py-tuntap-abi3`.

## Why this fork exists

- Keep the non-driver (`.dll`) portion buildable from open source in a repeatable GitHub Actions pipeline.
- Publish architecture-specific artifacts so downstream projects can ship only what they need.
- Support efficient Python wheel packaging by avoiding "all architectures in every wheel."

## What this fork builds and publishes

For each tagged release (for example `v0.14.1-dryark.18`), CI publishes:

- `drywintun-<upstream-version>-x64.zip`
- `drywintun-<upstream-version>-arm64.zip`
- `drywintun-<upstream-version>-x86.zip`
- `wintun-<upstream-version>.zip` (upstream reference package from `wintun.net`)

Each `drywintun-*.zip` bundle contains one architecture's files:

- `drywintun-<arch>.dll` (built in this repository)
- `DRYWINTUN-<ARCH>.sys` (extracted from upstream binary resources)
- `DRYWINTUN-<ARCH>.inf` (extracted from upstream binary resources)
- `DRYWINTUN-<ARCH>.cat` (extracted from upstream binary resources)

## What this accomplishes for Python wheels

Downstream wheel builders can fetch a single bundle per target architecture and include only:

- x64 Windows wheel -> x64 bundle
- arm64 Windows wheel -> arm64 bundle
- x86 Windows wheel -> x86 bundle

That keeps wheels architecture-specific and avoids wasting space by shipping unnecessary architectures.

## Build and release model

- Workflows run on GitHub-hosted `windows-2022` runners.
- Tags matching `v<major>.<minor>.<patch>-dryark.<n>` trigger release publication.
- The fork builds `drywintun.dll` from source.
- The workflow also fetches the corresponding upstream `wintun-<version>.zip` and extracts per-arch driver sidecars.

## Scope and intent

This fork is for transparent build/release automation and downstream packaging ergonomics. It is not presented as a replacement source of truth for upstream Wintun development.

## Licenses

- Source code in this repository follows upstream licensing terms (see `COPYING` and upstream notices).
- Upstream prebuilt binaries from `wintun.net` are provided under their own distribution terms in the upstream package.
