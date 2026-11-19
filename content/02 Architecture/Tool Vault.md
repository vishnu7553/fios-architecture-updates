---
title: Tool Vault
type: note
status: draft
tags: [fios/architecture, trust/trusted]
created: 2026-11-07
---
# Tool Vault

Up: [[Architecture]]

> **Summary:** Trusted, read-only manifests and docs for native tools, served by the warden and injected into context by the orchestrator.

## Source of truth
One folder per tool: `manifest.toml` plus `doc.md`. Installed under `/usr/lib/fios/tools/<class>/<tool>/` by the `fios` package, then built into a **hashed bundle**. Root-owned and read-only. See [[Arch Base]].

## Doc levels
| Level | Size | Content |
|---|---|---|
| **L0 index** | about 15 tokens | `win.focus W1 focus a window by id`. All L0 lines sit in the cached prefix |
| **L1 card** | about 120 tokens | Args, output, one example, gotchas |
| **L2 full** | about 500 tokens | Edge cases and the error table |

A build-time lint enforces the sizes.

## Rules
- Docs come only from the bundle, never from agent-writable paths or tool output.
- **Deviations only** for standard tools (`grep`, `sed`, ...): the model already knows them, so the vault documents only what is missing, capped, or class-restricted.
- **MCP tools:** descriptions are hash-pinned, changes are flagged, and the text is rewritten or summarized before it reaches the model. Never copied in verbatim.
- The warden only serves the bundle and holds no search code. The orchestrator ranks it (BM25 first). See [[Orchestrator]].
- The orchestrator reports the hashes of injected docs, and the warden logs them.

Related: [[Tool Contract]], [[Toolbox]], [[Invariants]] (9 and 10), [[Prompt Injection]].
