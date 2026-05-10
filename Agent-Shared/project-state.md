# Project State

## Active

### Hermes Agent (Falkenstein VPS, hermes user)
- Path: `/home/hermes/.hermes/`
- Codex (gpt-5.5) primary, no fallback
- WhatsApp gateway live (M's phone allowlisted)
- Skills: approval-scanner, soneri-banking-dashboard, inbox-triage, obsidian-memory (this skill)

### Soneri Banking Dashboard
- Sheet: https://docs.google.com/spreadsheets/d/1avhI_1M4eomw08EAyhdfEzWr2g2oE1IKTfMfReVrRUc
- Drive root: https://drive.google.com/drive/folders/1YZjbcmV_yZa-o2xNa_VUvhT9YL1utSMo
- 4,393 unique statements uploaded across 39 per-account folders
- Daily cron at 3pm Karachi: scan Gmail → parse PDFs → upload Drive → update Sheet
- 5,361 dups in `_dupes/` Drive folder

### Trading Bots (paper-only)
- Polymarket weather lag-arb scaffold: /home/hermes/polymarket-bot/
- Crosschain DEX arb scaffold: /home/hermes/crosschain-bot/
- Approval-gates skill: /home/hermes/.hermes/skills/approval-gates/

## Pending
- Tailscale auth (URL expired, need fresh)
- OCR install (apt broken on server)
- Identify ~165 unmapped accounts in Soneri parser output
