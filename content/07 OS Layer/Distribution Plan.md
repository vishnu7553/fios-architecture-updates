---
title: Distribution Plan
type: note
status: draft
tags: [fios/os]
created: 2026-11-07
---
# Distribution Plan

Up: [[OS Layer]]

> **Summary:** How FiOS ships: a thin Arch derivative delivered up a ladder, each rung useful on its own. The harness is the durable asset, and the distro is how it ships.

## Class of distro
FiOS is a **derivative** (like Omarchy, Kali, or Mint), not an independent distro (like Arch, Fedora, or Gentoo). Identity comes from purpose: a local-AI, guardrailed developer desktop.

## What we own
Warden, orchestrator, tool vault, rootfs allowlist, defaults, Quickshell UI, update pipeline, docs. See [[Architecture]].

## What we reuse
Kernel, libc, systemd, pacman, most packages, Hyprland, Quickshell, installer base.

## Ladder
| Rung | Ships | Notes |
|---|---|---|
| **R1** | Signed pacman repo with `fios` and `fios-settings` | Installable on existing Arch. Fastest way to let people try it |
| **R2** | Bootable VM or live image from `archiso`, rebuilt each milestone | The demo vehicle. Forces real integration of users, sockets, units |
| **R3** | Installable ISO: installer, LUKS, btrfs, Secure Boot decision, firmware | Only after the warden and orchestrator work |
| **R4** | Release cadence, docs, support channel, mirrors | Adoption, not engineering |

Almost nobody reinstalls their OS for an unknown distro's first release. They try a VM or install packages on what they already have.

## Open
- **Name:** FiOS collides with a well-known fiber brand. Decide before publishing a repo or domain. See [[ADR-0005 Names]].
- **Model weights:** download after install, not on the ISO.
- **Hardware and firmware** support is a long tail.

Related: [[Arch Base]], [[ADR-0009 Deliverable and Distribution Ladder]].