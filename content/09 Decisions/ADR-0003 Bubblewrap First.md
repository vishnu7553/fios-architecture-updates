---
title: ADR-0003 Bubblewrap First
type: adr
status: accepted
tags: [fios/decisions]
created: 2026-10-16
---
# ADR-0003 Bubblewrap First

Up: [[Decision Log]]

> **Summary:** Start with bubblewrap, swap incrementally.

**Status:** accepted

**Context:** simple and widely available sandboxing is needed now. Landlock is newer.

**Decision:** bubblewrap behind a `Sandbox` interface. Swap later without changing callers.

**Consequences:** mounts cannot be widened on a running sandbox, so session grants restart the session. See [[Sandbox]] and [[Grants and Approvals]].
