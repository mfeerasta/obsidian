# Decisions Log

## 2026-05-09
- Switched Hermes from /root to /home/hermes user (full isolation)
- Removed Anthropic Tabl key as fallback (Codex-only)
- Patched Hermes WhatsApp DM mention gating (`Hermes <msg>` to trigger)
- Allowlist M's phone + LID

## 2026-05-10
- Adopted SBL-<initials> <ccy> <last4> label scheme; RFB for Rupafab
- Fresh-downloaded all Soneri PDFs w/ unique filenames (`<msg_id>__<idx>__<base>.pdf`)
- Per-account dedup by (account, period_end), keep largest, rest → `_dupes/` Drive folder
- Added Account Number regex variant to parser; Statement-Date anchor for date-format detection
- Adopted Obsidian vault memory: `/Users/meerfeerasta/Claude/Claude` (Mac), Git-synced to `/home/hermes/obsidian-vault` (server)
