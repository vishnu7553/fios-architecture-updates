---
title: Non-Goals
type: note
status: draft
tags: [fios/vision]
created: 2026-10-16
---
# Non-Goals

Up: [[Vision]]

> **Summary:** Things deliberately out of scope for now, to prevent scope drift.

- Building an independent distro, package manager, or ISO before the execution layer is proven (see P5 in [[Phase Plan]]).
- An AI tool marketplace. It adds supply-chain risk and a cold-start problem.
- Multiple agents or multiple models at first. See [[ADR-0001 Single Model]].
- Any cloud dependency.
- Qubes-level isolation guarantees. A small team cannot honestly promise that.
- Wrapping all of Linux. Start with about 25 tools and grow only when the benchmark shows a gap. See [[Tool Contract]].
- 1-bit models for now. See [[Quantization and Paging]].
- Sophisticated voice. Push-to-talk and limited commands first.
