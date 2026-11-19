---
title: Approval UI
type: note
status: draft
tags: [fios/architecture, trust/trusted]
created: 2026-10-16
---
# Approval UI

Up: [[Architecture]]

> **Summary:** The human-in-the-loop surface, a Quickshell popup.

## Job
Show the user exactly what the agent wants and collect once, session, always, or deny.

## Rules
- A separate process from the orchestrator, on its own socket to the warden.
- Show the **exact** path, argv, or diff, never the model's explanation. Model text is untrusted.
- Group requests by directory and task to avoid prompt fatigue, because fatigue turns approval into "always click yes".
- Terminal fallback if the shell UI is unavailable.
- Approval binds to a plan hash. See [[Plan and Apply]].

## Open questions
Hardware-key confirmation for W2? See [[Open Questions]].


## Related
- [[Grants and Approvals]]
