---
title: Script Box
type: note
status: draft
tags: [fios/architecture, trust/untrusted]
created: 2026-11-07
---
# Script Box

Up: [[Architecture]]

> **Summary:** The throwaway sandbox where the model's bash runs. Only the [[Warden]] spawns and configures it.

## Job
Run the model's scripts (`sh.run`) with real bash and real tools, while the warden controls every effect that touches your files or system.

## What is inside
- **Rootfs:** bash plus an allowlist of tools (`grep`, `rg`, `sed`, `awk`, `find`, `git`, `jq`, `sort`, ...), built with `pacstrap` from the list in `rootfs/`. A tool not in the rootfs cannot run.
- **Native commands:** small stubs that call the warden (`win.list`, `ref.slice`, `calc`, `fs.*`). See [[Toolbox]].
- **Workspace:** only the granted subtree.
- **No network.** Limits on time, memory, output size, and tool calls per script.

## Modes
| Mode | Workspace | How writes work | When |
|---|---|---|---|
| **Read-only (v1)** | Read-only | `fs.*` stubs record effects, nothing executes | First build |
| **Clone (later)** | Copy-on-write clone | Real tools run on the clone, the diff is the plan | Build, test, and format workflows |

## Lifecycle (v1)
1. Orchestrator sends `sh.run`. The warden spawns the box with the session's mounts.
2. Bash runs. Globs expand over the read-only view, so file lists are concrete.
3. `fs.mv`, `fs.rm`, `fs.write`, `fs.edit`, `fs.mkdir` are recorded as effects.
4. Output returns capped, with a handle for anything large.
5. The effects become one aggregated plan bound to a hash. You approve it.
6. The warden snapshots, applies the effects, and destroys the box. See [[Plan and Apply]].

## Effect rules
- Each effect carries preconditions (file hash, destination absent) and a base ID.
- The warden resolves paths itself (symlinks, `..`) and checks scope at plan time and again at apply time.
- Apply is serialized. A failed precondition means abort and re-plan.
- A per-plan undo journal keeps prior contents. See [[Rollback and Snapshots]].
- Caps on `fs.write` size and hunks per plan. Bulk changes ask for confirmation.
- Large edits: the warden writes the proposed file to a scratch directory and runs allowlisted checks (syntax, lint) next to the diff.

## Limits (v1)
- A script cannot branch on the result of a write, because recorded writes only pretend to succeed.
- Tools that write into the tree (builds, tests, formatters) need clone mode.

## Not
- Not for desktop actions. Those go through native commands to the warden.
- Not escape-proof. The [[Red-Team Suite]] exists for this reason.
- Not the orchestrator's sandbox. See [[Sandbox]].

Related: [[Invariants]] (13: only the warden builds box configs), [[Tool Contract]], [[W2 Sandbox]], [[Arch Base]].
