---
title: Invariants
type: note
status: draft
tags: [fios/security]
created: 2026-10-16
---
# Invariants

Up: [[Security]]

> **Summary:** Thirteen rules that must always hold, each with a test idea.

| # | Invariant | Test idea |
|---|---|---|
| 1 | The orchestrator can reach nothing but the warden socket and the model socket | From inside the sandbox, try network, Hyprland socket, D-Bus, other sockets: all must fail |
| 2 | Identity comes from the kernel (`SO_PEERCRED`), never from message claims | A client claims another identity: rejected |
| 3 | Approval only arrives through the approval channel. Nothing the model emits counts | Model outputs text that looks like approval: ignored |
| 4 | An approval binds to a hash of the exact plan. Any change voids it | Modify a plan after approval: apply must fail |
| 5 | Every grant has an owner and an expiry. On warden restart all grants not in `policy.toml` are revoked | Kill the warden mid-grant, restart, retry access: denied |
| 6 | The warden never calls the model and only parses structured fields | Static check: no model client imported in `cmd/warden` |
| 7 | Guardrail files are root-owned and immutable, not writable by the agent | Agent attempts to write policy or tools: denied |
| 8 | The audit entry is written before the action runs | Crash between log and action: log shows the attempt |
| 9 | Tool docs come only from the vault bundle, never from tool output or the web | Point a tool at a fake doc: the injected text is never loaded |
| 10 | The orchestrator reports the hashes of injected docs, and the warden logs them | Inject a modified doc: the hash mismatch appears in the audit log |
| 11 | Every effect carries a precondition and a base ID; apply aborts on mismatch | Change a target after planning: apply is refused |
| 12 | Every applied transaction has a pre-image and a per-plan undo journal | Apply then undo: the prior contents return |
| 13 | Only the warden builds box configs | A session tries to supply its own mounts: rejected |

Related: [[Permission Classes]], [[Red-Team Suite]], [[W0 Threat Model and Spec]], [[Script Box]], [[Tool Vault]].
