---
title: Vision
type: moc
status: active
tags: [fios/vision]
created: 2026-10-16
---
# Vision

Up: [[Home]]

> **Summary:** Why FiOS exists, who it is for, and what it will do.

FiOS is a simple, clean, minimal Linux environment for developers like its author, packed with local AI. After install, the user can simply maintain their PC.

## What it should do
- Maintain the PC (updates, cleanup, diagnosing common problems).
- Offer a light voice assistant (not sophisticated).
- Automate debugging up to a limited level.
- Search the web, research, and investigate topics.
- Run **entirely locally**, with enough compute for a 3B to 7B model.

## What makes it different
- The OS itself is solid on security: guardrails, and protocols stating what may happen at each layer. See [[Security]].
- One model, not a swarm of agents. See [[ADR-0001 Single Model]].
- Everything the model sees is budgeted. See [[Output Discipline]].

## Time horizon
Long-term, about a year. It will be a drag at times, and the [[Roadmap]] exists so each step has a clear exit test.

## Map

- [[Principles]]: The rules every design choice is checked against.
- [[Non-Goals]]: Things deliberately out of scope for now, to prevent scope drift.
- [[Scope and Audience]]: Who FiOS is for and what hardware it assumes.
