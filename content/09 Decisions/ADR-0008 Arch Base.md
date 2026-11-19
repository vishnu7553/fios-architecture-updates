---
title: ADR-0008 Arch Base
type: adr
status: accepted
tags: [fios/decisions]
created: 2026-11-07
---
# ADR-0008 Arch Base

Up: [[Decision Log]]

> **Summary:** FiOS builds on Arch Linux as a thin derivative. Supersedes [[ADR-0004 Debian Nix Snapshots]].

**Status:** accepted (2026-11-07)

**Context:** Debian stable shipped without Hyprland, its backports looked fragile, and testing carries weaker security support plus transition churn. The warden, orchestrator, protocol, and vault are distro-independent, so the base choice only affects packaging and images.

**Decision:** Arch Linux (rolling) with `pacman`, `PKGBUILD`, `archiso`, and the Arch Linux Archive for pinned releases. btrfs plus snapper for rollback. No AUR in the shipped image.

**Alternatives considered:**
- Debian stable plus backports: stronger security story, more version juggling.
- Debian testing: packaged now, but slower and less predictable security.
- NixOS: strongest rollback, but a steep learning curve and a different packaging model.

**Consequences:**
- Easier packaging and image builds, and fresh desktop components.
- No stable branch. Secure Boot and MAC need our own work.
- Docs must not promise Debian-style stability.

**Checkpoint:** revisit if two rolling breakages block a release, or if a stable, security-team-backed promise becomes a requirement.

See [[Arch Base]] and [[Distribution Plan]].
