---
title: Linux Permission Mechanisms
type: note
status: draft
tags: [fios/security]
created: 2026-10-16
---
# Linux Permission Mechanisms

Up: [[Security]]

> **Summary:** The kernel tools available and their limits.

## Classic mode bits
Three sets (owner, group, others), each with read, write, execute. Only the first matching set applies. On directories: `r` lists, `w` creates or deletes entries, `x` enters.

## Layers beyond mode bits
- **Special bits:** setuid, setgid, sticky.
- **POSIX ACLs:** per-user and per-group rules beyond the three sets.
- **Capabilities:** splitting root's powers.
- **Immutable attribute (`chattr +i`):** protects the guardrail layer.
- **AppArmor:** optional on Arch, and as far as I know not enabled by default. FiOS relies on bubblewrap and the warden at first. SELinux is the alternative.
- **Landlock:** lets an unprivileged process restrict its own filesystem access. Candidate to replace bubblewrap later. See [[Sandbox]].
- **seccomp:** syscall filtering.

## Limits that shaped the design
- A denied `open()` returns `EACCES` and tells nobody. The ask step has to be built. See [[Grants and Approvals]].
- Removing an ACL does not revoke an already open file descriptor.
- The execute bit is weak for developer tools: granting exec on `python`, `bash`, `git`, or a compiler grants everything the agent user can do through them. Interpreters run in a sandbox with only the project mounted and no network.
- File permissions do not cover sockets, D-Bus, or the network. See [[Threat Model]].

## Mapping idea
| Class | Primary mechanism |
|---|---|
| R | dedicated user plus read-only bind mounts |
| W1, W2 | warden executes, agent has no write path at all |
| Denied | root ownership plus `chattr +i` plus no reachable path |


## Related
- [[Permission Classes]]
