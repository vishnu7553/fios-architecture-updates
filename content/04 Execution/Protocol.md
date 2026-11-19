---
title: Protocol
type: note
status: draft
tags: [fios/execution]
created: 2026-10-16
---
# Protocol

Up: [[Execution]]

> **Summary:** The socket messages between orchestrator, warden, and approval UI (v0).

JSON lines over Unix sockets: debuggable and fast to build.

| Message | Direction | Purpose |
|---|---|---|
| `call {tool, args}` | orchestrator to warden | Run a tool |
| `result {status, out or ref}` | warden to orchestrator | Output or handle |
| `denied {request_id, need}` | warden to orchestrator | Access missing, approval requested |
| `plan {id, hash, summary}` | warden to orchestrator | Dry-run result for a W action |
| `apply {id}` | orchestrator to warden | Execute an approved plan |

## Approval channel
A separate socket between the [[Approval UI]] and the [[Warden]]. Approvals never pass through the orchestrator.

## Example session
1. `call fs.read ~/work/foo/main.go` is denied by the sandbox.
2. Warden replies `denied {request_id: a7, need: {path, mode: r}}`.
3. UI shows the exact path, user picks "this session".
4. Warden restarts the session with the new mount. Agent retries and succeeds.
5. The audit log shows the whole chain.

## Auth
Caller identity from `SO_PEERCRED`. See [[Invariants]].
