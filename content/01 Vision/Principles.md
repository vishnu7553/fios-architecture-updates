---
title: Principles
type: note
status: draft
tags: [fios/vision]
created: 2026-10-16
---
# Principles

Up: [[Vision]]

> **Summary:** The rules every design choice is checked against.

1. **The model is never the security boundary.** The OS enforces every rule; the model works inside it. See [[Invariants]].
2. **Fail closed.** If the warden is down or confused, everything is denied.
3. **Reversible by default.** Writes snapshot first and can be undone. See [[Rollback and Snapshots]].
4. **Small trusted core.** Anything needing the model or complex parsing belongs outside [[Warden]].
5. **Context is expensive.** Pass references, not dumps. See [[Ref Store]].
6. **Measure, do not guess.** A fixed task benchmark decides whether a change helped. See [[Roadmap]].
7. **Local-first, no cloud.** No required network service.
8. **Start small, swap incrementally.** Example: bubblewrap first behind an interface. See [[ADR-0003 Bubblewrap First]].
9. **Promise less than you enforce.** Document exactly what is guaranteed.
