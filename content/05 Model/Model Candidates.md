---
title: Model Candidates
type: note
status: open
tags: [fios/model]
created: 2026-10-16
---
# Model Candidates

Up: [[Model]]

> **Summary:** Fill-in table for candidate models and measured results.

Fill this in as you test. Measure on the fixed task benchmark, not just public scores.

| Model | Size | Dense or MoE | Quant | RAM or VRAM | tok/s | Tool-call success on benchmark | Notes |
|---|---|---|---|---|---|---|---|
| (add) | | | | | | | |

## Questions per candidate
- Does it hold up at Q6 or higher for tool calls?
- Does it behave under grammar-constrained decoding?
- Does multi-turn degrade?
- Can it be fine-tuned with adapters on your own traces?

Related: [[Findings Log]], [[Quantization and Paging]].
