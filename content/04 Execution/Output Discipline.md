---
title: Output Discipline
type: note
status: draft
tags: [fios/execution]
created: 2026-10-16
---
# Output Discipline

Up: [[Execution]]

> **Summary:** Hard caps and handles so context never blows up.

## Rules
- Every tool has a hard output cap.
- Over the cap: a short summary plus a handle (`ref:o_41`). The full output goes to the [[Ref Store]].
- Generic read tools page through handles: `ref.slice`, `ref.grep`, `ref.head`.
- Formats are compact and line-oriented (TSV or short-key lines).

## Web and files
Search and fetch results are saved as handles. The model sees title plus a few lines and asks for pieces. This is the same mechanism the later retrieval layer will reuse: [[Hybrid Retrieval]].

## Why
A small model's context is the scarcest resource. The cheapest token is the one never sent. See [[Principles]].
