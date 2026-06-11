---
name: archie-health-2026-06
description: Live Archie (hermes) health audit Jun 2026 — both external channels down on auth/session expiry; cron state
metadata: 
  node_type: memory
  type: project
  originSessionId: 0b7d2d46-71b4-435e-9585-5da67e42f593
---

Read-only audit of the live Archie box (hermes, Tailscale 100.124.152.10) on 2026-06-10. See [[archie-website-funnel]], [[tenant-agents-layer]].

**Box state (good):** Hermes v0.16.0, gateway + dashboard:9119 both active (plan's upgrade/dashboard phases already done). 80 skills. `/root/.hermes` split-brain husk archived to `/root/backups/root-hermes-husk-20260610.tgz` and removed (single source of truth now). The 4 personal crons (hbl-monthly, archie-cdc-charges, personal-pk-monthly-accounts, asif-study) are registered in the home profile.

**RESOLVED 2026-06-10:** Both channels restored. Google token re-authed (new google_token.json, verified via gmail getProfile). WhatsApp re-paired. Crons meeting-prep/statement-intake/hourly-gmail-watcher resumed (recurring-bills stays paused for CLI rebuild). ROOT-CAUSE LESSON: `ssh hermes` lands as ROOT (Tailscale SSH --uid=0), so running `hermes whatsapp` over it wrote .env + whatsapp/session/creds.json root-owned -> gateway EACCES/PermissionError. Fix was `chown -R hermes:hermes /home/hermes/.hermes`. ALWAYS run hermes commands as the hermes user (`sudo -u hermes env HOME=/home/hermes ...`), never as root. Re-auth helper: /home/hermes/.hermes/scripts/google_reauth.py (--auth-url / --auth-code, PKCE-persisted).

**Original failures (now fixed):**
1. **WhatsApp bridge session dead.** Every cron delivery 500s: `Cannot destructure property 'user' of jidDecode(...)`. Bridge proc (`scripts/whatsapp-bridge/bridge.js --mode self-chat`) is up but lost its WhatsApp session. → re-pair (QR scan). This is the KEYSTONE: it also silences the gmail_token_check alert that would warn about #2.
2. **Google OAuth token revoked.** `invalid_grant: Token has been expired or revoked` (google_token.json, written Jun 8). Crashes all Gmail/Calendar crons. → re-auth: `cd ~/.hermes/skills/productivity/google-workspace/scripts && python3 setup.py --auth-url` then `--auth-code <CODE>` as meerfeerasta@gmail.com.

**Crons I PAUSED (un-pause after Google re-auth):** archie-meeting-prep (6e89a43809ad, was */5), archie-statement-intake (25ad35c81231, */15), Hourly Gmail urgent watcher (ecb742774392, 60m), archie-recurring-bills (4f8c213a01dd). Resume with `hermes cron resume <id>`.

**Still needs work:**
- **archie-recurring-bill-detector** (detect.py): CLI drift from v0.16 — calls `archie gmail search` (gmail is send-only now) and `archie drive upload` (only list/download/move exist). Needs a rebuild against the current CLI, not a quick fix. Left paused.
- **archie-sbl-monthly**: times out at global 120s default (no per-job timeout knob in this version); monthly, overran once Jun 3. Optimize the script.
- **PM2 daemon** under user hermes manages 0 apps (harmless idle); `sudo -u hermes pm2 kill` anytime. Bridge is standalone, not pm2-managed.
- v0.16.0 but 321 commits behind upstream; optional `hermes update --backup`.

**How to apply:** when M re-pairs WhatsApp + re-auths Google, resume the 4 paused crons and confirm deliveries land. The funnel/tenant code fixes from the prior session are committed in the repo but NOT yet deployed to the box.
