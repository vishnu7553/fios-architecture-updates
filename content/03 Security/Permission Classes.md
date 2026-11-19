---
title: Permission Classes
type: note
status: draft
tags: [fios/security]
created: 2026-10-16
---
# Permission Classes

Up: [[Security]]

> **Summary:** R, W1, W2, and Denied, enforced by the OS, not by naming.

| Class | Meaning | Examples | Enforcement | Approval |
|---|---|---|---|---|
| **R** | Pure observation | list windows, read file, search index, system status | Separate unprivileged user, read-only mounts, no network | None |
| **W1** | Reversible change in the user's own space | focus a window, edit a file in the workspace, move a file | [[Warden]] executes, snapshot first, undo available | Policy decides; ask for everything at first |
| **W2** | System or irreversible change | install a package, edit `/etc`, delete outside the workspace, send data out | Warden only, plan and apply | Always human confirmation |
| **Denied** | Auth, keys, bootloader, the guardrail layer | n/a | Unreachable by design | n/a |

## Two caveats
1. **R is not automatically safe.** Reading `~/.ssh`, browser profiles, or `.env` can leak secrets, and a file or web page can contain instructions aimed at the model. R needs path deny-lists and untrusted marking.
2. **Classify wrappers, not binaries.** `git status` takes an index lock and `find -exec` runs commands. The model gets wrappers with a fixed argument grammar, so each tool's class is true by construction. See [[Tool Contract]].

## Workspace and deny-list (defaults)
Workspace is `~/work/` plus explicitly granted directories. Dotfiles and a secrets deny-list (`.ssh`, `.env`, browser profiles) stay out. See [[ADR-0007 Approval Defaults]].

## Mapping to Linux mechanisms
See [[Linux Permission Mechanisms]].
