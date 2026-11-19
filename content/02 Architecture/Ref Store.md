---
title: Ref Store
type: note
status: draft
tags: [fios/architecture]
created: 2026-10-16
---
# Ref Store

Up: [[Architecture]]

> **Summary:** Handles for large outputs so context stays small.

## Idea
When a tool output exceeds its cap, the warden saves it to a file and returns a short summary plus a handle such as `ref:o_41`.

## Generic read tools
`ref.slice`, `ref.grep`, `ref.head` page through a handle on demand.

## Uses
- Logs, large diffs, directory listings.
- Web pages: the fetcher saves cleaned text and returns a title plus a few lines. See [[Hybrid Retrieval]].

## Safety
Content from files and the web is marked untrusted. See [[Prompt Injection]].

## Location
`/var/lib/fios/refs/`. See [[Output Discipline]].
