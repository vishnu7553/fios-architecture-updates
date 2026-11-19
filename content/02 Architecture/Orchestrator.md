---
title: Orchestrator
type: note
status: draft
tags: [fios/architecture, trust/untrusted]
created: 2026-10-16
---
# Orchestrator

Up: [[Architecture]]

> **Summary:** The untrusted agent loop and the first component to build. It talks to the model, assembles context, keeps history, retrieves and injects tool docs, and sends every action to the [[Warden]]. It is disposable: kill it and restart it, and nothing security-critical is lost.

## Job
- Talk to the [[Model Server]] and run the agent loop.
- Own context assembly, conversation history, and compaction. See [[Context and Compaction]].
- Rank and inject tool docs from the [[Tool Vault]].
- Send every action to the warden (`sh.run`, `tx.*`, `tool.call`). See [[Protocol]].
- Handle `denied` replies: wait for approval, then retry. See [[Grants and Approvals]].
- Run the browse and act sessions on the same weights.

## Trust
Untrusted by design. It runs in the [[Sandbox]] as `fios-agent` and can reach only the warden socket and the model socket. It holds no secrets, no policy, and no authority. Every capability comes from a warden-issued session token.

## Sessions
One model, two contexts with different permissions. See [[ADR-0001 Single Model]] and [[Prompt Injection]].

| Session | Token allows | Never |
|---|---|---|
| **Act** | `sh`, `tx`, `tool.call` | web access |
| **Browse** | `web.*`, `ref.*`, docs | `sh`, `tx` |

The warden rejects any call outside the session's token, even if injected text makes the model emit one. Data crosses sessions only as typed artifacts through the warden, marked untrusted.

## Modules
| Module | Job |
|---|---|
| `modelclient` | Streaming, stop conditions, constrained decoding, tokenizer access |
| `context` | Assembly in a cache-friendly order, token accounting per region |
| `history` | Append-only conversation log (source of truth), compaction jobs |
| `docs` | Loads the vault bundle, ranks (BM25 first, embeddings later), injection policy |
| `loop` | State machine with step and retry limits |
| `lint` | Advisory bash lint with one-line fixes. The [[Script Box]] is the real guarantee |
| `sessions` | Browse and act contexts, token handling |
| `router` (later) | Fast path for trivial commands without the model |

## Context layout
```
[stable prefix]  rules + L0 tool index        cached, never edited
[summary]        compacted older turns
[recent turns]   calls, results, handles
[injections]     L1/L2 docs as tool-role messages, hash-tagged, budgeted
```
- Append-only between compactions. Compaction rewrites only the summary region.
- Inject at turn boundaries, never inside unfinished reasoning.
- Docs come only from the vault bundle, never from tool output or the web.

## Agent loop
Observe, decide, act, read the result, then stop or retry, under hard step, retry, and token limits.

| Warden reply | Orchestrator does |
|---|---|
| `ok` | Add the result to context |
| `ref` | Keep the handle, not the content |
| `denied` | Surface the request, wait for approval, retry |
| `plan` | Show the plan, wait for approval, then `plan.apply` |
| `error` | Add the one-line fix and inject the named doc, then retry within limits |
| `busy` | Poll the job handle, do not spin |

## Doc injection
Triggers, most reliable first: pre-turn ranking on the user's request, error-triggered injection, an explicit `tool.help`, then mid-stream keywords as an experiment only. Starting budgets: about 400 injected tokens per turn and a working set of about 1,200 per session. Inject each doc once, evict least-recently-used, and on compaction drop L2 and keep L0.

## Not allowed
- Import warden internals. The only shared code is the `protocol` message types.
- Hold secrets or policy.
- Treat any model output as approval.
- Write the tool vault or its bundle.
- Run commands except through the warden.

## Failure behavior
- Warden unreachable: halt and report.
- Model server down: retry within limits, then report.
- Session token rejected: stop that session and log it, never retry with another token.
- Crash: the warden kills its boxes and revokes its grants. On restart, rebuild context from `history` and resume a transaction by ID if one exists.

## Open issues
- Language: Go to start. JSONL keeps Python possible later.
- Call format, see the experiment below.
- Whether reasoning text stays in history.
- The compaction method and its trigger.

---

# Implementation Strategies

## Principles
1. **Contract first.** Freeze protocol v0 (verbs, message shapes, error format) before writing orchestrator code.
2. **Fake the warden.** A test double speaks the protocol so the orchestrator can be built and benchmarked now. It is never shipped and never gets real authority.
3. **Baseline before features.** Get a naive loop working, measure it, then add one feature at a time and measure each.
4. **Record and replay.** Store raw model outputs and replay them to test the loop, parser, and context code deterministically, with no model needed.
5. **Sandboxed from day one.** Even before the real warden exists, run the orchestrator under bubblewrap with only the two sockets mounted and no network, so nothing depends on ambient access.
6. **No agent frameworks.** Context control is the product, and frameworks hide it. Use the standard library plus a few small libraries.

## Build order
| Step | Build | Exit test |
|---|---|---|
| **O0** | Protocol v0 written down | A fake warden and orchestrator can talk from the doc alone |
| **O1** | CLI skeleton plus fake warden | A scripted dialogue runs end to end with a canned model |
| **O2** | Model client plus a naive loop: act session only, single `sh` tool, no compaction | Completes 3 simple tasks on your real model, full transcripts saved |
| **O3** | Eval harness: the 20 tasks, metrics, record and replay, temperature 0 | Baseline numbers logged in [[Findings Log]] |
| **O4** | Docs: L0 prefix, then pre-turn retrieval, then error-triggered injection, then `tool.help` | Each step beats or matches the baseline on tokens or success |
| **O5** | History and compaction | A simulated 200-turn session stays inside budget and passes a recall check |
| **O6** | Browse and act sessions with tokens | A page containing fake instructions causes no act-side call |
| **O7** | Swap in the real warden | The same benchmark, with no regression except approval latency |

## Model backend
- Run inference as a **separate process** behind a `ModelClient` interface, with no embedding at first. llama.cpp's server is the likely candidate. As far as I know it offers a chat endpoint, streaming, grammar or JSON-schema constraints, prompt-cache reuse, and a tokenize endpoint. Verify each in the docs for your build.
- Count tokens with the model's own tokenizer, not estimates.

## KV-cache discipline
- No timestamps or changing data in the prefix.
- Keep context append-only between compactions.
- Log the cached prefix length and prompt-eval time every turn. These show whether your layout helps or hurts.

## Experiment: call format
Putting bash inside a JSON string means escaping quotes and newlines, which small models often get wrong. Compare:
- **A:** JSON function call, `{"tool":"sh","args":{"script":"..."}}`.
- **B:** a fenced `sh` block that the orchestrator parses, with the mode in a header line.

Measure parse failures and task success. The protocol to the warden stays JSON either way, because the orchestrator re-encodes it.

## Experiment: reasoning text
Hypothesis: strip thinking text from history after each turn and keep only calls, results, and summaries. Test success against tokens.

## Package layout
```
fios/
  cmd/orchestrator/     main and CLI
  internal/orch/        modelclient, context, history, docs, loop, lint, sessions
  internal/protocol/    shared message types only, no policy code
  internal/fakewarden/  test double, test builds only
  eval/                 tasks, runner, metrics, recordings
```

## Risks
- **Building features before the baseline exists.** Then nothing can be judged.
- **The fake warden drifting from the real one.** Keep a protocol conformance test that runs against both.
- **Scope creep into the router, memory, and voice.** All are parked for now.
- **Bad habits formed without a sandbox.** Run sandboxed from O1.