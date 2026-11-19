---
title: OS Layer
type: moc
status: active
tags: [fios/os]
created: 2026-10-16
---
# OS Layer

Up: [[Home]]

> **Summary:** The base system: Arch Linux, the desktop, rollback, distribution, and hardware.

Base: Arch Linux as a thin derivative, with Hyprland and Quickshell. Rollback through btrfs snapshots before write actions. Shipped as packages first, then a VM image, then an ISO. See [[ADR-0008 Arch Base]]. The earlier Debian plan is kept for history in [[ADR-0004 Debian Nix Snapshots]].

## Map

- [[Arch Base]]: Arch Linux as a thin derivative, and what it implies.
- [[Distribution Plan]]: How FiOS ships, as a ladder of rungs.
- [[Desktop Hyprland and Quickshell]]: How the desktop pieces are used and their risks.
- [[Rollback and Snapshots]]: Every write can be undone: snapshots before W actions.
- [[Hardware Profile]]: Fill in your machine. Several decisions depend on it.