---
title: Sandbox
type: note
status: draft
tags: [fios/security]
created: 2026-10-16
---
# Sandbox

Up: [[Security]]

> **Summary:** Default-deny containment for agent sessions, starting with bubblewrap.

## Choice
Bubblewrap first, behind a Go `Sandbox` interface (`Start(session, mounts)`, `Stop`) so it can be swapped for Landlock later. See [[ADR-0003 Bubblewrap First]].

## Baseline for an agent session
Default deny. Only the workspace and the warden and model sockets are visible. No network. No access to `$HOME` beyond what is mounted.

## Flags to review carefully in W2
`--unshare-all`, `--unshare-net`, `--die-with-parent`, `--new-session`, `--clearenv`, `--ro-bind`, `--bind`, `--tmpfs`, `--proc`, `--dev`, `--seccomp`. A single missing flag can silently weaken isolation, so review the exact command line. See [[W2 Sandbox]].

## Key limitation
Bubblewrap fixes its mounts at startup and cannot widen a running sandbox. So:
- **"Once" grants:** the warden opens the file and passes the file descriptor over the socket.
- **"Session" and "always" grants:** restart the session with updated mounts. This is cheap if the model session is stateless and real state lives in the daemon and the log.

## Prerequisites
Unprivileged user namespaces must be enabled on the target install. Verify Arch's stock kernel.

## Related
[[Grants and Approvals]], [[Linux Permission Mechanisms]], [[Red-Team Suite]].
