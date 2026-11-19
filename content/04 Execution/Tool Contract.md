---
title: Tool Contract
type: note
status: draft
tags: [fios/execution]
created: 2026-10-16
---
# Tool Contract

Up: [[Execution]]

> **Summary:** Every tool declares what it is, what it may touch, and how much it returns.

## Manifest (readable with `tool --describe`)
```toml
name = "win.list"
class = "R"
summary = "List open windows: id, app, title, workspace"
args = { workspace = "optional int" }
output = { format = "tsv", max_lines = 40 }
```
W tools add `dry_run = true`, `undo = "..."`, and `scope = [...]`.

## Rules
- **Wrappers, not binaries.** Fixed argument grammar, so the class is true by construction. See [[Permission Classes]].
- **Progressive disclosure.** The model sees a one-line index of tool names and summaries and requests the full manifest only for the tool it intends to use.
- **Keep the total small:** about 25 tools to start, 30 to 50 at most, because every extra tool costs a small model attention. Naming: `domain.verb`.
- **Stable short IDs:** `w3`, `f12`. Never long addresses or raw JSON blobs.
- **Errors are model-sized:** one line plus the likely fix.
- **Long-running jobs return a handle** with a `job.status` command from day one.

## Open question
How compact can a manifest be before accuracy drops? See [[Open Questions]].

Related: [[Toolbox]], [[Tool Vault]], [[Output Discipline]].
