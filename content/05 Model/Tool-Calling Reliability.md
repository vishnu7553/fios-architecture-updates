---
title: Tool-Calling Reliability
type: note
status: draft
tags: [fios/model]
created: 2026-10-16
---
# Tool-Calling Reliability

Up: [[Model]]

> **Summary:** Why small models fail at agent work and how to compensate.

## Findings from reading (verify before relying)
- One survey found models below 3B can pick the right tool but cannot reliably form arguments or sequence multi-step operations. Treat 3B as the floor.
- Single-turn function calling is largely saturated in benchmarks. Multi-turn state handling is where models separate.
- Tool use is a trained capability, so a model trained for it can beat a larger one that was not.

## Compensations
- Constrain output with grammars (llama.cpp GBNF or JSON schema). See [[Shell Design]].
- Keep the tool set small and descriptions short. See [[Tool Contract]].
- Return diffs from actions so the model needs no verify round trip.
- Fix the harness before changing the model if the benchmark fails.

Sources: [[Sources]].
