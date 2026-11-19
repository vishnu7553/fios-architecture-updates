---
title: Quantization and Paging
type: note
status: draft
tags: [fios/model]
created: 2026-10-16
---
# Quantization and Paging

Up: [[Model]]

> **Summary:** Ways to fit more model into less memory, and what was learned.

## Native 1-bit (BitNet b1.58)
- Trained from scratch with ternary weights, not quantized after training. You cannot shrink an existing model this way.
- Needs a specialized kernel (`bitnet.cpp`) and does not run on standard llama.cpp.
- The 2B4T model's card advises against real-world use without further testing.
- Verdict: revisit when a native 1-bit model at 7B with tool-calling training exists.

## Post-training quantization
Standard INT4 and similar. Lower quants may corrupt tool-call tokens: one source recommends Q6 or higher for tool calling. Single source, so test it yourself.

## Paging, in practice: MoE expert streaming
- MoE models activate few experts per token, so expert weights can be streamed from SSD instead of held in RAM.
- One prototype reports about 4.7 tok/s using about 2 GB of RAM on Qwen3-30B-A3B. Fine for background jobs, too slow for voice.
- llama.cpp has flags to place expert tensors on CPU (`--n-cpu-moe`, `--override-tensor`), and mmap gives part of the benefit by default.
- Treat as an optional tier, not the default.

## Dense models
No such sparse trick. Every token touches all weights, so layer paging from disk is slow.

Sources: see [[Sources]]. Related: [[Model Candidates]].
