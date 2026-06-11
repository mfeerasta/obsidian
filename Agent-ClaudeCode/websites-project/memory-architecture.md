---
name: memory-architecture
description: "Where memory lives. Claude Code memory vs Archie's Obsidian vault are SEPARATE; Obsidian is NOT connected to this Claude Code."
metadata: 
  node_type: memory
  type: reference
  originSessionId: e5377b22-a7ba-4a0e-a66d-8ef60de63cac
---

Two separate memory systems are in play. They are NOT connected to each other (checked 2026-06-11). See [[archie-health-2026-06]], [[website-business]].

**1. Claude Code (this CLI) — native file memory.** Everything I save lives in `~/.claude/projects/-Users-meerfeerasta-Desktop-AI-Projects-Websites/memory/*.md` + `MEMORY.md` index. This IS actively recording our work every session (it's how all these memory notes exist). It is NOT an Obsidian vault, NOT git-synced, and has NO Obsidian MCP wired in (`~/.claude.json` has no obsidian server).

**2. Archie / Hermes — Obsidian vault (its memory backbone).** Server clone at `/home/hermes/obsidian-vault` (11 notes), canonical copy on M's Mac in **iCloud** (`iCloud~md~obsidian`), git-synced between them. Archie uses the `obsidian-memory` (4-layer recall) + `obsidian-rag` skills against it. So Obsidian learns what **Archie** does, not what **this Claude Code** does. (The iCloud vault wasn't downloaded/visible on the Mac at check time; fd found no `.obsidian` under ~.)

**Bottom line for M's question:** Obsidian is connected to Archie, not to Claude Code. The rich session memory I write is in Claude Code's own store, separate from the vault. **Gap:** our Claude-Code work does not flow into Obsidian today. **To bridge** (if M wants Obsidian to learn what we do here): either (a) add an Obsidian MCP to this Claude Code, or (b) mirror/sync the `memory/*.md` files into a folder in the Obsidian vault and git-push so both Obsidian and Archie see them. Not done yet, offered.
