---
title: Prompt Injection
type: note
status: draft
tags: [fios/security]
created: 2026-10-16
---
# Prompt Injection

Up: [[Security]]

> **Summary:** The central threat for an LLM agent, and the design response.

## What it is
The model cannot reliably tell instructions from data inside its own context. A web page or file read at the user's request enters the context as ordinary content, and its text can steer the model.

## Why encryption does not fix it
Encryption and SSH-style keys prove who sent a message and that it was not altered in transit. Injection involves no impersonation: the attacker's text arrives legitimately, as data the user asked to read. The model must see plaintext, so a decryption layer only authenticates the user's message and cannot stop the model from obeying unsigned text next to it.

## Where the idea does apply
At the warden layer, where code can enforce it:
- An approval token that signs a hash of the exact plan, so the model cannot forge or swap it.
- An authenticated approval channel (trusted UI, hardware key for W2).
- Speaker verification for voice, which blocks background audio but not injected text.

## Design response (make injection harmless)
- Session split with one model: the browsing session has network and no file or shell access. The action session has local access and no network. They exchange only structured, validated data. See [[Orchestrator]].
- Egress allowlists per service.
- Mark file and web content as untrusted at the protocol level.
- Every write passes through the [[Warden]] with human approval. See [[Plan and Apply]].

## Open research
Current prompt-injection defenses and instruction/data separation methods were not researched in the planning conversation. See [[Open Questions]].


## Related
- [[Threat Model]]
- [[Invariants]]
