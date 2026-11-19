---
title: Threat Model
type: note
status: draft
tags: [fios/security]
created: 2026-10-16
---
# Threat Model

Up: [[Security]]

> **Summary:** Assets, actors, attack paths, and what is out of scope.

## Assets
User files and source code, secrets (SSH keys, `.env`, browser profiles, tokens), system integrity, the guardrail layer itself, the audit log.

## Actors and inputs
- **Malicious web content** read by the research session.
- **Malicious file content** (a README or log containing instructions aimed at the model).
- **Background audio** reaching the voice input (a video playing can speak commands).
- **A confused or compromised model**: wrong tool calls, bad arguments.
- **Local malware** running as the user.
- **Third-party tools** if a marketplace ever exists (out of scope for now, see [[Non-Goals]]).

## Attack paths to design against
| Path | Mitigation |
|---|---|
| Injection leads to command execution | Session split, sandbox, plan and apply, human approval. See [[Prompt Injection]] |
| Injection leads to exfiltration | Network off in the action session, egress allowlists |
| Secret read leads to leak | Path deny-list, R is not automatically safe. See [[Permission Classes]] |
| Bypass through IPC sockets | Agent cannot reach Hyprland, D-Bus, tmux, or SSH-agent sockets. See [[State Daemon]] |
| Privilege escalation | No setuid, `sudo`, or docker group access for the agent user |
| Symlink races (TOCTOU) | Warden opens paths itself and passes file descriptors |
| Lingering grants | Expiry plus revoke-on-restart. See [[Grants and Approvals]] |
| Voice command injection | Voice reaches only R and W1-ask without confirmation. See [[Invariants]] |
| Agent edits its own rules | Guardrail files root-owned and immutable (`chattr +i`) |

## Out of scope (stated honestly)
Kernel exploits, physical access, a malicious root user, hardware attacks.

## Assumptions to verify
Unprivileged user namespaces enabled on the Arch kernel (bubblewrap needs them; verify). See [[Sandbox]].
