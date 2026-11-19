---
title: Model Server
type: note
status: draft
tags: [fios/architecture]
created: 2026-10-16
---
# Model Server

Up: [[Architecture]]

> **Summary:** Local inference process, unprivileged and offline.

## Role
Runs the chosen model (currently expected to be llama.cpp based) and serves only the orchestrator.

## Rules
- Unprivileged user, no network.
- Reachable only over a local socket from the [[Orchestrator]].
- Model choice is the author's personal research track. See [[Model]].

## Options to evaluate
Dense 3B to 7B, MoE with expert streaming, adapters or full fine-tune. See [[Model Candidates]] and [[Quantization and Paging]].
