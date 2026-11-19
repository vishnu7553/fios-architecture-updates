---
title: Context and Compaction
type: note
status: needs improvement
tags:
  - fios/memory
created: 2026-10-16
Finalized: Nope
---
# Context and Compaction

Up: [[Memory]]

> **Summary:** Keep the conversation log forever, send the model only a small curated window.

## Principles
- The append-only log is the source of truth. Context is a cache over it.
- Compaction: summarise older turns when context nears its limit.
- Structured note-taking: the model writes persistent notes outside its context and reads them back later.
- Progressive disclosure: load detail just in time through tools instead of pre-loading.

## Known techniques named in reading
Compaction, structured note-taking, and sub-agent style fresh contexts with careful handoffs. Sub-agent style maps to restarting a session with a summary on the same model.

## Test
Recall across simulated weeks of use (P3 exit test in [[Phase Plan]]).

Related: [[Orchestrator]], [[Failure Memory]].
