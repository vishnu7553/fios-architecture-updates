---
title: W2 Sandbox
type: milestone
status: later
tags: [fios/roadmap]
created: 2026-10-16
---
# W2 Sandbox

Up: [[Roadmap]]

> **Summary:** Bubblewrap launcher behind an interface, orchestrator stub inside.

**Goal:** a sandboxed session that can reach only the warden socket.

**Deliverables:** `internal/sandbox` with a `Sandbox` interface and a bubblewrap implementation, orchestrator stub running inside it, first [[Red-Team Suite]] tests.

**Exit test:** the stub cannot read `$HOME`, cannot reach the network, and cannot touch the Hyprland or D-Bus sockets (one test each).

**Depends on:** [[W1 Warden Skeleton]]. **Next:** [[W3 R Tools and Ref Store]].
