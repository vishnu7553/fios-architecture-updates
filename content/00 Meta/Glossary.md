---
title: Glossary
type: note
status: draft
tags: [fios/meta]
created: 2026-10-16
---
# Glossary

Up: [[Home]]

> **Summary:** Project vocabulary in one place.

| Term | Meaning |
|---|---|
| **FiOS** | FRIDAY Integrated Operating System, the project name. |
| **FRIDAY** | Name of the model. The acronym itself is undecided. |
| **warden** | Trusted core daemon (Go) that enforces policy and executes approved actions. See [[Warden]]. |
| **orchestrator** | Untrusted agent loop that talks to the model, sandboxed. See [[Orchestrator]]. |
| **R / W1 / W2** | Permission classes: read, reversible write, system or irreversible write. See [[Permission Classes]]. |
| **Handle / ref** | A pointer like `ref:o_41` to a large output stored on disk. See [[Ref Store]]. |
| **Plan / apply** | Dry run produces a plan with an ID and hash, then apply executes it. See [[Plan and Apply]]. |
| **Grant** | A permission given to the agent for once, a session, or always. See [[Grants and Approvals]]. |
| **Reference monitor** | A small, always-invoked, tamper-proof component that mediates access. The warden's role. |
| **Prompt injection** | Untrusted text in the model's context that the model treats as instructions. See [[Prompt Injection]]. |
| **MoE** | Mixture of Experts model, only some experts active per token. See [[Quantization and Paging]]. |
| **Backronym** | An acronym invented after the name. |
