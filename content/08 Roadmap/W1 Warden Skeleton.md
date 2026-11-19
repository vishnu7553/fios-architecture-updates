---
title: W1 Warden Skeleton
type: milestone
status: later
tags: [fios/roadmap]
created: 2026-10-16
---
# W1 Warden Skeleton

Up: [[Roadmap]]

> **Summary:** Socket, peer-credential auth, audit log, policy loader, deny-all.

**Goal:** a Go daemon that authenticates peers and denies everything by default.

**Deliverables:** `cmd/warden`, `internal/proto` with `SO_PEERCRED`, `internal/audit` append-only log, `internal/policy` loader reading `policy.toml`.

**Exit test:** unknown peers are rejected and every request is logged.

**Depends on:** [[W0 Threat Model and Spec]]. **Next:** [[W2 Sandbox]].
