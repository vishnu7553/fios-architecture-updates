---
title: Sentinel
type: note
status: draft
tags: [fios/architecture, trust/trusted]
created: 2026-11-07
---
# Sentinel

Up: [[Architecture]]

> **Summary:** The warden's action watcher. It counts what sessions do and trips a circuit breaker. It never reads model text.

## Job
Watch **actions, not thoughts.** Detect runaway or suspicious behavior from the counts of calls the [[Warden]] already sees.

## Signals
- Calls per minute per session.
- Repeated denials of the same request.
- The same call repeated in a loop.
- Tool calls per script and boxes spawned per hour.

## Breaker actions
Pause the session, kill its boxes, and alert the user through the [[Approval UI]]. Thresholds live in `policy.toml`.

## Rules
- It reads only metadata and counters, never model prose or script text.
- Every trip is logged to the audit log before it acts.
- If the sentinel cannot run, new sessions are denied (fail closed).

## Open
Starting thresholds, to tune on the benchmark. See [[Open Questions]].

Related: [[Invariants]], [[Architecture]].
