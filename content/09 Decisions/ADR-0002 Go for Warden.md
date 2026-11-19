---
title: ADR-0002 Go for Warden
type: adr
status: accepted
tags: [fios/decisions]
created: 2026-10-16
---
# ADR-0002 Go for Warden

Up: [[Decision Log]]

> **Summary:** Warden language is Go.

**Status:** accepted

**Context:** the warden is the most security-critical code and must stay small and auditable.

**Decision:** Go, memory-safe, simple concurrency, good Unix socket support.

**Consequences:** the orchestrator can be any language but must only speak the [[Protocol]]. See [[Warden]].
