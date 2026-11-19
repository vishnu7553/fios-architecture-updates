---
title: ADR-0005 Names
type: adr
status: accepted
tags: [fios/decisions]
created: 2026-10-16
---
# ADR-0005 Names

Up: [[Decision Log]]

> **Summary:** Component and project names.

**Status:** accepted, revisit before public release

**Decisions:**
- **warden**: trusted reference monitor. "Broker" was weak and "orchestrator" would invite scope creep because an orchestrator coordinates rather than guards.
- **orchestrator**: the untrusted agent loop.
- **FiOS**: FRIDAY Integrated Operating System.
- **FRIDAY**: model name. Acronym undecided. Candidates: Framework for Reasoning, Inspection, Diagnostics, Automation, Yours; Fully-local Reasoning Interface for Developers, Automation, Yours.

**Risks:** FiOS is a well-known fiber internet brand, which hurts discoverability and may cause trademark confusion in a public release. FRIDAY is also a fictional character's name. Treat both as internal names for now.

See [[Warden]], [[Orchestrator]], [[Glossary]].
