---
title: Rollback and Snapshots
type: note
status: draft
tags: [fios/os]
created: 2026-10-16
---
# Rollback and Snapshots

Up: [[OS Layer]]

> **Summary:** Every write can be undone: snapshots before W actions, plus an undo journal for file effects.

## Mechanism
- btrfs snapshots before every W1 and W2 action, managed by the [[Warden]]. Snapper is the likely tool. Candidate: `snap-pac` for snapshots around pacman transactions (verify).
- File effects also write a per-plan undo journal with prior contents, because rolling back a snapshot would also undo other legitimate changes.

## Update pipeline (`fios update`)
Snapshot, full upgrade from the pinned source, migrations, health checks, roll back on failure. Privileged steps are W2 actions through the warden.

## Rules
- If the snapshot fails, abort the action.
- Snapshot protects data and config. It is weaker than NixOS generation rollback.
- Never do partial upgrades.
- Keep snapshot tooling a first-class part of the warden, not an afterthought.

## Open
Retention policy and disk budget. See [[Open Questions]].

Related: [[Plan and Apply]], [[Arch Base]], [[ADR-0008 Arch Base]].