---
title: ADR-0004 Debian Nix Snapshots
type: adr
status: superseded
tags: [fios/decisions]
created: 2026-10-16
---
# ADR-0004 Debian Nix Snapshots

Up: [[Decision Log]]

> **Summary:** Debian base, btrfs snapshots for rollback. Superseded by [[ADR-0008 Arch Base]] on 2026-11-07.

**Status:** superseded by [[ADR-0008 Arch Base]]

**Context:** wanted a Nix-like approach and rollbacks instead of plain apt, but starting from stock Debian.

**Decision:** Debian base. Nix as a package manager for agent-managed tooling. Rollback through btrfs snapshots before every write.

**Consequences:** weaker than NixOS generations. If snapshots prove inadequate, revisit NixOS or an immutable base. See [[Arch Base]] and [[Rollback and Snapshots]].

**Why superseded:** the architecture does not depend on the distro. Hyprland and Quickshell are native to Arch, `PKGBUILD` packaging is simpler for a solo maintainer, and Debian testing carries security-support and transition-churn costs. Debian now packages both, so this was a fit decision, not forced by availability. The btrfs snapshot idea carries over. The Nix idea is dropped.
