---
title: ADR-0007 Approval Defaults
type: adr
status: proposed
tags: [fios/decisions]
created: 2026-10-16
---
# ADR-0007 Approval Defaults

Up: [[Decision Log]]

> **Summary:** Four proposed defaults for approval and workspace.

**Status:** proposed. Accept or change each, then mark accepted.

1. **Approver:** the Quickshell popup with a terminal fallback. It shows the exact path, argv, or diff, never the model's explanation. See [[Approval UI]].
2. **W1:** ask for everything at first. Relax per tool only after the audit log shows it behaving. See [[Permission Classes]].
3. **Workspace:** `~/work/` plus explicitly granted directories. Dotfiles and a secrets deny-list (`.ssh`, `.env`, browser profiles) stay out by default.
4. **Warden unreachable:** fail closed, so every action is denied. See [[Invariants]].

**Consequences:** safer but more prompts at first, which is why prompts are grouped by directory and task. See [[Grants and Approvals]].
