---
title: Plan and Apply
type: note
status: draft
tags: [fios/execution]
created: 2026-10-16
---
# Plan and Apply

Up: [[Execution]]

> **Summary:** Two-step writes: a reviewable plan, then a gated execution.

## Flow
1. A tool with `--dry-run` produces a plan (diff or action list), a plan ID, and a hash.
2. The user approves via the [[Approval UI]]. The approval binds to the hash.
3. `apply <plan-id>` goes to the [[Warden]], which verifies the hash, checks policy against the class, takes a snapshot, executes, and returns a diff of what changed.
4. The audit entry is written before execution and completed after. See [[Invariants]].

## Failure rules
- If the snapshot fails, abort the apply.
- If the plan changed since approval, abort.
- Undo restores from the snapshot. See [[Rollback and Snapshots]].

Related: [[Permission Classes]], [[W5 Plan Apply and Snapshots]].
