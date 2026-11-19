---
title: Warden
type: note
status: draft
tags: [fios/architecture, trust/trusted]
created: 2026-10-16
---
# Warden

Up: [[Architecture]]

> **Summary:** The trusted reference monitor. Decide, execute, log. Nothing else.

## Job
Receive requests from the orchestrator, check them against policy and permission class, ask for approval when needed, take a snapshot, execute, return a diff, and write an audit entry **before** acting.

## Language and size
Go. Keep it tiny and memory-safe. It is the most security-critical code in the project and must stay auditable. See [[ADR-0002 Go for Warden]].

## It does
- Authenticate peers via `SO_PEERCRED`.
- Classify and gate actions: [[Permission Classes]].
- Manage grants and expiries: [[Grants and Approvals]].
- Run plan and apply: [[Plan and Apply]].
- Launch and stop sandboxes: [[Sandbox]].
- Own the audit log and the [[Ref Store]].

## It never does
- Call the model.
- Parse free-form model prose. Only structured fields.
- Grow planning, retry, or conversation logic. That belongs in [[Orchestrator]].

## Failure behavior
Fail closed. On restart, revoke all grants not written in `policy.toml`. See [[Invariants]].

## Why this name
It was previously called "broker" and "orchestrator" was rejected because an orchestrator coordinates, while this component guards. See [[ADR-0005 Names]].

## Tests
Unknown peers rejected, every request logged, killing the warden mid-grant leaves no access. See [[W1 Warden Skeleton]] and [[W4 Grants and Approval]].
