---
title: Desktop Hyprland and Quickshell
type: note
status: draft
tags: [fios/os]
created: 2026-10-16
---
# Desktop Hyprland and Quickshell

Up: [[OS Layer]]

> **Summary:** How the desktop pieces are used and their risks.

## Hyprland
Wayland compositor in C++ with dynamic tiling. Useful here through IPC: `hyprctl` over a socket queries windows and workspaces and dispatches commands, and an event socket streams window and workspace events. It moves fast and breaks between versions, so expect to chase interface changes. Recent versions may use an in-house backend library instead of wlroots (verify in the repo).

**Risk:** `hyprctl dispatch exec` can launch commands as the desktop user, so the agent must never reach the socket directly. See [[Threat Model]].

## Quickshell
A toolkit for status bars, widgets, lockscreens, and other desktop components on Qt6 and QtQuick. It supports Wayland and X11, integrates with PipeWire, MPRIS, system tray, PAM, and Bluetooth, has Hyprland- and Sway-specific features, and uses declarative QML with live reload.

Used here as a display surface (the [[Approval UI]], status panels) and possibly a source of shell state. It is a client of the warden, not the tool bus. Do not put logic in QML.

To verify:
- Its IPC, in the docs.
- Whether it can act as a polkit agent. The 0.3.0 Debian packaging lists polkit agent build dependencies. This could matter for the Approval UI and for approval authenticity (see [[Threat Model]]).

## Packaging
Native to Arch (verify official repos versus AUR). Both are also packaged in Debian testing as of Nov 2026, with slower updates. See [[Arch Base]].

## Wayland basics (why it matters)
Clients cannot see each other, and screen capture and global shortcuts need explicit protocols or portals. That fits a permissioned design. Compositor protocol support varies.

Related: [[State Daemon]].