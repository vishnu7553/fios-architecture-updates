---
title: Model
type: moc
status: active
tags: [fios/model]
created: 2026-10-16
---
# Model

Up: [[Home]]

> **Summary:** Model research track. Owned personally by the author; results land here.

One model, 3B or 7B depending on need, possibly small specialist models for voice and screenshots later. The author is researching this personally (dense vs MoE, full fine-tune vs adapters) and will record results here. The [[Warden]] does not depend on the model choice.

## Constraints
- Local only, limited compute. See [[Hardware Profile]].
- It must call tools reliably. See [[Tool-Calling Reliability]].
- It runs for long periods, so memory and context matter. See [[Memory]].

## Map

- [[Model Candidates]]: Fill-in table for candidate models and measured results.
- [[Quantization and Paging]]: Ways to fit more model into less memory, and what was learned.
- [[Tool-Calling Reliability]]: Why small models fail at agent work and how to compensate.
- [[Findings Log]]: Dated log of your own model experiments.
