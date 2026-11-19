---
title: Phase Plan
type: note
status: draft
tags: [fios/roadmap]
created: 2026-10-16
---
# Phase Plan

Up: [[Roadmap]]

> **Summary:** P0 to P5 with exit tests.

| Phase | Build | Exit test |
|---|---|---|
| **P0** (month 1) | Threat model, layer protocol, tool schema, 20-task benchmark, metrics | Harness runs a naive baseline and produces numbers |
| **P1** (months 2-3) | State daemon, read-only tools, progressive disclosure, self-describing manifests | Fewer tokens and higher success than baseline on the benchmark |
| **P2** (months 4-5) | Execution layer (file, command, snapshots, confirmation, audit), sandboxed fetcher writing to files not context | A suite of hostile web pages triggers no W action |
| **P3** (months 6-7) | Memory tiers, compaction, failure log | Recall tests pass across simulated weeks |
| **P4** (months 8-9) | Push-to-talk voice, screenshot fallback | Voice commands reach only R and W1-ask without confirmation |
| **P5** (months 10-12) | Image build, installer, updates, model by hardware | Clean install on three machines |

## Risks
- No benchmark means nothing can be judged.
- Scope drift toward P5.
- Small-model unreliability: fix the harness first.

Related: [[Non-Goals]], [[Red-Team Suite]].
