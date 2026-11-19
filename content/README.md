# FiOS Vault

Obsidian vault for **FiOS (FRIDAY Integrated Operating System)**: a minimal, security-first, Arch-based distro with a local AI assistant.

## Open it
1. Obsidian, Open folder as vault, choose this folder.
2. Open `Home.md`. Every branch of the vault is linked from there as a mind map.
3. Templates and Graph view are already enabled, and the Templates folder is preconfigured. The dedicated diagram is `FiOS Architecture.canvas`, which uses the `advanced-canvas` community plugin.

## Use it
Read `00 Meta/How to Use This Vault.md` first. Short version: look at NOW only, capture new ideas in the Parking Lot, update Where Was I at the end of a session.

## Git
```
git init && git add . && git commit -m "Initial FiOS vault"
```

## Structure
```
Home.md
FiOS Architecture.canvas   visual mind map of the whole vault
00 Meta/          working rules, now-next-later, parking lot, glossary, re-entry note
01 Vision/        why, principles, non-goals, scope
02 Architecture/  warden, orchestrator, script box, tool vault, approval UI, state daemon, toolbox, ref store, sentinel, model server
03 Security/      threat model, invariants, permission classes, sandbox, grants, injection, Linux permission mechanisms, red team
04 Execution/     tool contract, output discipline, plan and apply, shell design, protocol
05 Model/         candidates, quantization and paging, tool-calling reliability, findings log
06 Memory/        hybrid retrieval, context and compaction, failure memory (paused)
07 OS Layer/      Arch Linux, desktop, rollback, distribution, hardware profile
08 Roadmap/       phase plan P0-P5, milestones W0-W6
09 Decisions/     decision log and ADRs 0001-0009
10 Research/      sources and open questions
Templates/        ADR, milestone, research, daily, idea
.obsidian/        preconfigured settings (templates folder, core plugins, graph)
```
