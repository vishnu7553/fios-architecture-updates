---
title: Security
type: moc
status: active
tags: [fios/security]
created: 2026-10-16
---
# Security

Up: [[Home]]

> **Summary:** What must never happen, and how the OS enforces it.

The security stance is one sentence: **the model is never the security boundary.** The kernel and the [[Warden]] enforce every rule. If the model is fooled, it still cannot do damage.

## Reading order
1. [[Threat Model]]: assets, attackers, attack paths.
2. [[Invariants]]: the rules that must always hold, each testable.
3. [[Permission Classes]]: R, W1, W2, Denied.
4. [[Sandbox]] and [[Linux Permission Mechanisms]]: how the kernel enforces it.
5. [[Grants and Approvals]]: how a human unlocks access.
6. [[Prompt Injection]]: the central threat and why design beats encryption.
7. [[Red-Team Suite]]: the tests that keep the claims honest.

## Honest framing
"Solid security" is a promise that has to be kept with patches, audits, and a written threat model. Promise less and document exactly what is enforced.

## Map

- [[Threat Model]]: Assets, actors, attack paths, and what is out of scope.
- [[Invariants]]: Thirteen rules that must always hold, each with a test idea.
- [[Permission Classes]]: R, W1, W2, and Denied, enforced by the OS, not by naming.
- [[Linux Permission Mechanisms]]: The kernel tools available and their limits.
- [[Sandbox]]: Default-deny containment for agent sessions, starting with bubblewrap.
- [[Grants and Approvals]]: How a human unlocks access, and how grants expire safely.
- [[Prompt Injection]]: The central threat for an LLM agent, and the design response.
- [[Red-Team Suite]]: Escape attempts run from W2 onward so the invariants are tested, not claimed.


## Related
- [[Architecture]]
- [[Execution]]
