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

**BRIDGE BUILT (2026-06-11) — both done:**
- The Mac Obsidian vault is `/Users/meerfeerasta/Claude/Claude` (NOT iCloud; found via `~/Library/Application Support/obsidian/obsidian.json`). It's a git repo, remote `github.com/mfeerasta/obsidian`, branch main, with `Agent-Hermes/` (Archie) + `Agent-OpenClaw/` folders. The Hermes clone (`/home/hermes/obsidian-vault`) is the same repo.
- **Mirror + push:** `~/.claude/sync-memory-to-obsidian.sh` rsyncs this project's `memory/*.md` → vault `Agent-ClaudeCode/websites-project/` → git commit + `push origin main` (use `git pull --rebase --autostash` first; other machines push to the same repo). Ran it: 22 files mirrored + pushed. So Claude Code memory now flows into Obsidian (app sees it on disk) and to Archie (on next pull). Re-run the script to re-sync.
- **Obsidian MCP added** to Claude Code user config (`~/.claude.json`): `npx -y obsidian-mcp /Users/meerfeerasta/Claude/Claude` (StevenStavrakis filesystem-based, no Obsidian-app/plugin needed). **Activates on next Claude Code session start** (MCP servers load at startup), not mid-session.
