---
title: Toolbox
type: note
status: draft
tags: [fios/architecture]
created: 2026-10-16
---
# Toolbox

Up: [[Architecture]]

> **Summary:** The set of wrapper commands and manifests, sorted by R, W1, W2.

## What lives here
`/usr/lib/fios/tools/{r,w1,w2}/` with wrappers and a manifest per tool, root-owned and read-only.

## Rules
- Wrap, do not expose raw binaries. See [[Tool Contract]].
- Each tool declares its class, scope, args, output cap, and for W tools a dry run and undo.
- About 25 tools to start, 30 to 50 maximum, grouped by domain: `win`, `fs`, `proc`, `sys`, `pkg`, `web`, `mem`, `dev`.

## Related
[[Permission Classes]], [[Tool Vault]], [[Output Discipline]], [[Plan and Apply]].
