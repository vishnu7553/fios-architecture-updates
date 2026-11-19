---
title: Memory
type: moc
status: paused
tags: [fios/memory]
created: 2026-10-16
---
# Memory

Up: [[Home]]

> **Summary:** Long-running context and recall. Deferred until OS, tools, and model are settled.

The assistant runs for days, weeks, maybe years. Context is a cache over a permanent log. The plan: a hybrid of exact search (grep) and semantic search (vectors), reused for conversation history, long-term notes, and web results.

This track is **deliberately paused** until the OS and tools and the model are settled. See [[Roadmap]].

## Map

- [[Hybrid Retrieval]]: Grep for the specific, vectors for the fuzzy, one mechanism for everything.
- [[Context and Compaction]]: Keep the conversation log forever, send the model only a small curated window.
- [[Failure Memory]]: Learn from mismatches between expected and actual results, without training.
