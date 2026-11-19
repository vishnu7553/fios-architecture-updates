---
title: Decision Log
type: moc
status: active
tags: [fios/decisions]
created: 2026-10-16
---
# Decision Log

Up: [[Home]]

> **Summary:** Index of architecture decision records (ADRs).

One note per decision, using [[ADR Template]]. Status values: proposed, accepted, superseded.

| ADR | Decision | Status |
|---|---|---|
| [[ADR-0001 Single Model]] | One model, several sessions | accepted |
| [[ADR-0002 Go for Warden]] | Warden written in Go | accepted |
| [[ADR-0003 Bubblewrap First]] | Bubblewrap behind an interface | accepted |
| [[ADR-0004 Debian Nix Snapshots]] | Debian plus btrfs snapshots | superseded by ADR-0008 |
| [[ADR-0005 Names]] | warden, orchestrator, FiOS, FRIDAY | accepted, revisit before public release |
| [[ADR-0006 Fresh Start]] | No existing code carried over | accepted |
| [[ADR-0007 Approval Defaults]] | Four default approval rules | proposed |
| [[ADR-0008 Arch Base]] | Arch Linux thin derivative | accepted |
| [[ADR-0009 Deliverable and Distribution Ladder]] | Harness is the asset, shipped via a ladder | proposed |

## Map

- [[ADR-0001 Single Model]]: One model, not separate agents.
- [[ADR-0002 Go for Warden]]: Warden language is Go.
- [[ADR-0003 Bubblewrap First]]: Start with bubblewrap, swap incrementally.
- [[ADR-0004 Debian Nix Snapshots]]: Debian base, btrfs snapshots for rollback. Superseded by ADR-0008.
- [[ADR-0005 Names]]: Component and project names.
- [[ADR-0006 Fresh Start]]: No earlier code is carried over.
- [[ADR-0007 Approval Defaults]]: Four proposed defaults for approval and workspace.
- [[ADR-0008 Arch Base]]: FiOS builds on Arch Linux as a thin derivative.
- [[ADR-0009 Deliverable and Distribution Ladder]]: The harness is the durable asset. The distro ships it up a ladder.
