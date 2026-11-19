---
title: Shell Design
type: note
status: open
tags: [fios/execution]
created: 2026-10-16
---
# Shell Design

Up: [[Execution]]

> **Summary:** How the model's bash runs: in the [[Script Box]], with only recorded effects touching the host. A purpose-built structured shell remains a later option.

## Idea
A small command language over a socket as the single choke point for classification, output caps, dry-run, snapshots, and audit. v1 instead runs real bash inside the [[Script Box]] and records effects; this structured shell is a later optimization.

```
win.list | where app~firefox | first      # R
fs.find "*.log" in ~/proj | grep ERROR    # R; large output returns ref:o_7
fs.edit src/main.go --patch p1 --dry-run  # W1; returns plan:p9
apply p9                                  # snapshot, policy check, run, diff
```

## Benefits
One tool in the schema, filtering in code (`where`, `first`), no quoting-based injection (the model's bash is confined to the [[Script Box]]), and grammar-constrained decoding (llama.cpp GBNF) so a small model cannot emit malformed syntax.

## Costs and risks
- Models are trained on bash, so a novel syntax may cost accuracy. Keep it close to verb-noun commands, pipes, and flags.
- Shells are a tarpit: omit loops, functions, and variables at first.
- Long-running jobs need handles and `job.status`.
- Check whether an existing structured shell such as Nushell can be extended before writing a parser. Not yet evaluated.

## Build order
1. Protocol first as plain argv over a socket: [[Protocol]].
2. Add the pipe grammar only if the benchmark shows token savings.
3. Add constrained decoding when the grammar is stable.

## Arbitrary commands
No raw host bash. The model's scripts run only inside the [[Script Box]], an allowlisted rootfs with no network and no host write path; `fs.*` effects are recorded and applied through plan and apply. Native commands outside the box are argv-style exec against a per-class allowlist. Anything else runs in a throwaway [[Sandbox]] (no network, scratch overlay) and only the resulting diff can be promoted to a real W1 or W2 action. See [[Script Box]] and [[W6 Exec and Red Team]].
