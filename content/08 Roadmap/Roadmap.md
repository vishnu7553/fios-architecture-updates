---
title: Roadmap
type: moc
status: active
tags: [fios/roadmap]
created: 2026-10-16
---
# Roadmap

Up: [[Home]]

> **Summary:** The order of work, with an exit test at every step.

Two views of the same plan: the long phases and the shorter execution and guardrail track.

- [[Phase Plan]]: P0 to P5 over about a year.
- Execution track: [[W0 Threat Model and Spec]] to [[W6 Exec and Red Team]].
- [[Distribution Plan]]: R1 to R4 ladder. R1 and R2 run alongside P1 to P4, R3 starts at P5.

## Rule
Do not start P5 (the distro image) until the P2 exit test passes. The distro is the most visible part and the least important until the execution layer holds.

## Map

- [[Phase Plan]]: P0 to P5 with exit tests.
- [[W0 Threat Model and Spec]]: Write the threat model, invariants, and protocol spec.
- [[W1 Warden Skeleton]]: Socket, peer-credential auth, audit log, policy loader, deny-all.
- [[W2 Sandbox]]: Bubblewrap launcher behind an interface, orchestrator stub inside.
- [[W3 R Tools and Ref Store]]: Read tools, output caps, handles.
- [[W4 Grants and Approval]]: Denial as signal, fd passing, session restart, Quickshell approval.
- [[W5 Plan Apply and Snapshots]]: Plan and apply for W1 and W2 with btrfs snapshots and undo.
- [[W6 Exec and Red Team]]: Argv allowlist, throwaway sandbox, diff promotion, full red-team pass.
