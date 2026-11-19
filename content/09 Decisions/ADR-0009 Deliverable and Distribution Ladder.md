---
title: ADR-0009 Deliverable and Distribution Ladder
type: adr
status: proposed
tags: [fios/decisions]
created: 2026-11-07
---
# ADR-0009 Deliverable and Distribution Ladder

Up: [[Decision Log]]

> **Summary:** The durable asset is the harness. The distro ships it up a ladder of rungs.

**Status:** proposed (awaiting confirmation of the "distro-shaped, not distro-sized" reading)

**Context:** the stated goal was a full distro from the start. A full distro carries a long tail (installer, hardware, security response) that can absorb the project before the harness is proven.

**Decision:** package and build like a distro from day one (R1: signed repo, R2: a bootable image each milestone). Defer the installer, branding, and hardware polish (R3, R4) until the warden and orchestrator work.

**Consequences:** integration problems surface early, there is always something demonstrable, and nothing in the harness depends on the installer.

See [[Distribution Plan]] and [[Roadmap]].
