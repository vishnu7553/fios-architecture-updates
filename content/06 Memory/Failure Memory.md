---
title: Failure Memory
type: note
status: paused
tags: [fios/memory]
created: 2026-10-16
---
# Failure Memory

Up: [[Memory]]

> **Summary:** Learn from mismatches between expected and actual results, without training.

## Idea
Log `(state, action, expected diff, actual diff)` for every action. Mismatches become short lessons keyed by app or tool. Retrieve the one or two relevant lessons into context before acting.

## Why
This is a non-parametric version of "minimise loss and remember what caused failures", and it fits a small local model. It needs no fine-tuning.

## Connections
- The reasoning-loop idea: a fixed loop (observe, decide intent, act, read the diff, stop or retry) plus swappable domain knowledge, here the desktop.
- Invariants checked by code, not by the model: for example, closing a window must change focus or window count.
- Depends on actions returning diffs. See [[Plan and Apply]].

Related: [[Hybrid Retrieval]].
