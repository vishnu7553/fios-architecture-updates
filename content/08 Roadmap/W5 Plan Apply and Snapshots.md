---
title: W5 Plan Apply and Snapshots
type: milestone
status: later
tags: [fios/roadmap]
created: 2026-10-16
---
# W5 Plan Apply and Snapshots

Up: [[Roadmap]]

> **Summary:** Plan and apply for W1 and W2 with btrfs snapshots and undo.

**Goal:** every write is reviewable and reversible.

**Deliverables:** plan and apply, hash-bound approvals, snapshot integration, undo. See [[Plan and Apply]] and [[Rollback and Snapshots]].

**Exit test:** apply then undo restores state, and a failed snapshot aborts the apply.

**Checkpoint:** if snapshots prove inadequate, revisit NixOS or an immutable base ([[Arch Base]]).

**Depends on:** [[W4 Grants and Approval]]. **Next:** [[W6 Exec and Red Team]].
