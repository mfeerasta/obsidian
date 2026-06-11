---
name: feerasta-incorporations
description: "The 5 services built from the Claude Research folder — what shipped, where, how to run"
metadata: 
  node_type: memory
  type: project
  originSessionId: 0b7d2d46-71b4-435e-9585-5da67e42f593
---

Built 2026-06-07 from the `~/Downloads/Claude Research` analysis (see `~/Desktop/claude-research-incorporation-plan.pdf`). All new files, dry-run/mock by default, no live billed calls, guardrails encoded. lead-engine typecheck green; package.json scripts wired. Nothing committed yet.

- **A · Aria restaurant vertical** → `portfolio-site/aria/restaurants/index.html` (teal/coral, own SEO, 0 Feerasta) + `lead-engine/docs/aria-restaurant.md` (system prompt, Voiceflow+ManyChat+Twilio+Cal.com stack, Meta 24h rules, walk-in script). NB: Google Business Messages is dead (July 2024) — not used; "Xavier"=ManyChat.
- **B · Local-SEO audit (Ascent)** → `lead-engine/src/local-seo-audit.ts` (`bun run local-seo-audit --slug <slug> [--pdf]`, mock unless AHREFS_API_KEY/GSC_ACCESS_TOKEN), `migrations/0002-local-seo-audits.sql`, `docs/local-seo-playbook.md` (4-area stack, 10-wk plan, audit $750-1,200 / retainer $1,500-2,500/mo 6-mo min). FTC review-rule boundary encoded.
- **C · Invoice Chaser (Intelligence)** → `lead-engine/src/invoice-chaser.ts` (`bun run invoice-chaser`, dry-run mock; --live reads Stripe/QBO READ-ONLY), `migrations/0003-invoice-chaser.sql`, `docs/invoice-chaser.md`. Hard guardrail: never move money, draft+queue only, owner sends; engagement-letter language + E&O note. $300-600/mo.
- **D · Brand Voice Capture (Studio/Ascent)** → `lead-engine/src/brand-voice-capture.ts` (`bun run voice --client <slug>`, dry-run sample → ~200-word profile in `voice-profiles/`), `docs/brand-voice/*` (interview + compiler prompts, template, README). $300-500 one-time, lock-in. Keep profile ~200 words not 5k tokens.
- **E · Self-maintaining second brain (Intelligence MVP)** → `lead-engine/src/second-brain/{index,workflows}.ts` (`bun run brain-all`, dry-run), `migrations/0004-second-brain.sql`, `docs/second-brain.md`. 5 workflows (briefing/capture/review/queue/health) on Postgres growth schema + Archie cron; aligns with [[feerasta-brochure]] intelligence demo. Dogfood internally first.

Do-first order (from the plan): D (this week) → B → cheap-model router + skill library → A → C (needs QBO app assessment + E&O) → E. Router/skill-library/Paperclip/repos = internal margin+velocity levers, not yet built.

## Deployed to Archie/Hermes 2026-06-07
4 of these now live as Hermes Agent skills on hermes (`/home/hermes/.hermes/skills/`, registered + enabled), modeled on `website-funnel` (agentic, draft-only, approval-gated): **local-seo-audit** (Ascent, FTC review boundary), **invoice-chaser** (Intelligence, read-only/never-move-money), **brand-voice-capture** (Studio/Ascent), **aria-receptionist** (Aria orphan, ops/sales playbook — receptionist itself runs external Voiceflow+ManyChat+Twilio, NOT hermes). Plus a **Feerasta house memory** `memories/feerasta/INDEX.md` (+ MEMORY.md pointer) mapping all 5 divisions + 2 orphans + pricing + the legacy-name reconciliation (Feerstone=Studio, Local-AI=Sovereign/Enterprise) so Archie understands the whole company. Autonomous crons wired 2026-06-07, all PAUSED (enable when ready): `ascent-local-seo-weekly` (Mon 05:00 UTC, skill local-seo-audit), `intelligence-invoice-chaser-weekly` (Mon 05:30 UTC, skill invoice-chaser), `aria-monthly-reports` (1st 06:00 UTC, skill aria-receptionist) — agentic, draft-only, WhatsApp brief to M (deliver whatsapp:12488286124@s.whatsapp.net). brand-voice-capture = on-demand only (one-time client intake, no cron). To enable: `hermes cron resume <id>`. invoice-chaser needs Stripe/QBO wired before live. See [[archie-website-funnel]] for the unified Hermes platform.
