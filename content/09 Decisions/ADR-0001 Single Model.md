---
title: ADR-0001 Single Model
type: adr
status: accepted
tags: [fios/decisions]
created: 2026-10-16
---
# ADR-0001 Single Model

Up: [[Decision Log]]

> **Summary:** One model, not separate agents.

**Status:** accepted

**Context:** limited compute, and complexity grows quickly with multiple models.

**Decision:** one model (3B or 7B by requirement). Isolation is done with separate **sessions** of the same weights that have different OS permissions, not different models. Small specialist models for voice and screenshots may come later.

**Consequences:** sessions run one after another on small hardware. Security rests on the OS, not on model separation. See [[Orchestrator]] and [[Prompt Injection]].
