---
title: ADR-0006 Fresh Start
type: adr
status: accepted
tags: [fios/decisions]
created: 2026-10-16
---
# ADR-0006 Fresh Start

Up: [[Decision Log]]

> **Summary:** No earlier code is carried over.

**Status:** accepted

**Decision:** start the new design clean, with no existing code carried over.

**Consequence:** the earlier approach to execution isolation is replaced by a real [[Sandbox]], because process separation alone does not separate privileges. See [[Roadmap]].
