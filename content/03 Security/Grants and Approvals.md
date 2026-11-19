---
title: Grants and Approvals
type: note
status: draft
tags: [fios/security]
created: 2026-10-16
---
# Grants and Approvals

Up: [[Security]]

> **Summary:** How a human unlocks access, and how grants expire safely.

## Mechanism
Denial as signal: the sandboxed agent tries something, it fails, the [[Warden]] records the denial and replies `denied` with a request ID, the [[Approval UI]] asks the user, and the agent retries after approval.

## Alternatives considered
| Approach | Note |
|---|---|
| fanotify permission events | Real blocking prompts, needs privileges, can hang or deadlock |
| seccomp user notification | Flexible, easy to get wrong (TOCTOU), supervisor must open the path itself |

Start with denial as signal. It matches how models handle "denied, retry later".

## Grant types
| Type | Implementation |
|---|---|
| Once | File descriptor passed by the warden |
| Session | Sandbox restarted with updated mounts, ends with the session |
| Always | Written to `policy.toml`, reviewable by the user |

## Rules
- Every grant has an owner and an expiry.
- On warden restart, revoke everything not in `policy.toml`.
- Approval binds to the plan hash. See [[Plan and Apply]].
- The prompt shows the exact path, argv, or diff.
- Beware prompt fatigue and prompts crafted by an injected model. See [[Prompt Injection]].

## Do not use
`chmod` or `setfacl` grants. A crash would leave them behind permanently.

Related: [[Approval UI]], [[Invariants]], [[W4 Grants and Approval]].
