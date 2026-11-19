---
title: Execution
type: moc
status: active
tags: [fios/execution]
created: 2026-10-16
---
# Execution

Up: [[Home]]

> **Summary:** How the model's actions actually run, safely and cheaply.

Execution is where the model stops reading and starts changing things: read files, write files, run commands. Everything here goes through the [[Warden]].

## Core ideas
- Tools are wrappers with manifests: [[Tool Contract]].
- Big outputs become handles: [[Output Discipline]].
- Writes are plan then apply: [[Plan and Apply]].
- Arbitrary commands run in the throwaway [[Script Box]]; only a diff can be promoted. See [[Shell Design]].
- Messages follow one small protocol: [[Protocol]].

## Map

- [[Tool Contract]]: Every tool declares what it is, what it may touch, and how much it returns.
- [[Output Discipline]]: Hard caps and handles so context never blows up.
- [[Plan and Apply]]: Two-step writes: a reviewable plan, then a gated execution.
- [[Script Box]]: Where the model's bash runs, with recorded effects and no host write path.
- [[Shell Design]]: Idea: a purpose-built agent shell served by the warden. Decide after the protocol works.
- [[Protocol]]: The socket messages between orchestrator, warden, and approval UI (v0).


## Related
- [[Security]]
- [[Architecture]]
