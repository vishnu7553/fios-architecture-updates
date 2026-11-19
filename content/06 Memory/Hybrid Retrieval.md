---
title: Hybrid Retrieval
type: note
status: paused
tags: [fios/memory]
created: 2026-10-16
---
# Hybrid Retrieval

Up: [[Memory]]

> **Summary:** Grep for the specific, vectors for the fuzzy, one mechanism for everything.

## Idea
- Exact lookups: full-text search (grep, SQLite FTS5).
- Fuzzy concepts: embeddings and semantic search.
- Return **handles and short snippets**, never dumps. See [[Output Discipline]].

## Reuse
The same pipeline serves conversation recall, notes, and web research: fetched pages go through the [[Ref Store]], get indexed, and the model asks for the top few results.

## Constraints
Indexing runs while the machine is idle so it does not fight inference. Keep the index in SQLite for simplicity.

## Open
Which of the five known memory mechanism families is simplest and passes the recall test? See [[Open Questions]] and [[Sources]].
