---
title: Arch Base
type: note
status: draft
tags: [fios/os]
created: 2026-10-16
---
# Arch Base

Up: [[OS Layer]]

> **Summary:** FiOS is a thin derivative of Arch Linux. We reuse Arch's kernel, packages, and tooling and own only the harness, defaults, and desktop integration.

## Decision
Arch Linux (rolling) with `pacman`. See [[ADR-0008 Arch Base]]. The Debian plan it replaced is in [[ADR-0004 Debian Nix Snapshots]].

## Why Arch
- Hyprland and Quickshell are first-class and current. Verify official repos versus AUR for each.
- `PKGBUILD` is far simpler to maintain than `.deb` packaging, which matters for a solo maintainer.
- `archiso` builds images and `pacstrap` builds the rootfs for the [[Script Box]].
- The Arch Linux Archive gives dated repo snapshots for reproducible builds.
- Precedent: Omarchy is an Arch derivative built this way (two packages, a curated list, an ISO, an update command that snapshots first). Verify details in its repo.

## Tooling map
| Need | Tool |
|---|---|
| Package format | `PKGBUILD` |
| Our repo | Signed pacman repository (`repo-add`) |
| Image build | `archiso` |
| Script-box rootfs | `pacstrap` with the allowlist from `rootfs/` |
| Pinning | Arch Linux Archive snapshot per release |
| Rollback | btrfs plus snapper. See [[Rollback and Snapshots]] |
| Our packages | `fios` (warden, orchestrator, vault) and `fios-settings` (system files) |

## Rules
- **No AUR in the shipped image.** AUR packages are unreviewed user scripts, a supply-chain risk. If we need one, we build it and publish it in our own repo.
- **No partial upgrades.** Images come from one consistent snapshot, and updates are full upgrades.
- **Update pipeline (`fios update`):** snapshot, full upgrade, migrations, health checks, roll back on failure. Privileged steps are W2 actions through the [[Warden]].

## Costs to accept
- **No stable branch.** Fixes arrive fast but so does everything else. Docs must not promise Debian-style stability.
- **Secure Boot.** As far as I know, Arch has no signed shim by default. Options: user-enrolled keys (for example `sbctl`) or no Secure Boot support in early rungs. Not yet verified.
- **MAC is not default.** AppArmor and SELinux are optional, so FiOS relies on bubblewrap and the warden at first.
- **Rolling breakage** depends on the snapshot and rollback path working.

## To verify on the install
- Unprivileged user namespaces enabled (bubblewrap needs them). See [[Sandbox]].
- Filesystem layout supports btrfs snapshots.
- Hyprland and Quickshell come from the official repos or our own repo, not the AUR.
- Secure Boot approach decided for each rung of [[Distribution Plan]].

## Longer term
If snapshots prove inadequate, revisit NixOS or an immutable base at the end of [[W5 Plan Apply and Snapshots]].

## Checkpoint
Revisit the base only if two rolling breakages block a release, or if a stable, security-team-backed promise becomes a requirement.