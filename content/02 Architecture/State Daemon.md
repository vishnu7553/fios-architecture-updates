---
title: State Daemon
type: note
status: draft
tags: [fios/architecture]
created: 2026-10-16
---
# State Daemon

Up: [[Architecture]]

> **Summary:** Cheap, always-fresh knowledge of the desktop so the model never polls.

## Job
Keep a live in-memory model of windows, workspaces, focus, notifications, media, and battery without calling the model.

## Sources
- Hyprland event socket and `hyprctl` queries. See [[Desktop Hyprland and Quickshell]].
- D-Bus (read only).
- Possibly Quickshell state. Verify its IPC in the docs before relying on it.
- AT-SPI for widget-level info later. Coverage is patchy: Chromium and Electron need accessibility flags and games expose nothing.

## Interface
Read tools (class R) answer from the cache in milliseconds, for example `win.list`. See [[Tool Contract]].

## Disclosure levels
Level 0: one-line summary. Level 1: window list. Level 2: one window's interactive elements. Level 3: screenshot as a last resort.

## Important
The agent must never talk to the Hyprland socket directly, because `hyprctl dispatch exec` can launch commands as the desktop user. See [[Threat Model]].
