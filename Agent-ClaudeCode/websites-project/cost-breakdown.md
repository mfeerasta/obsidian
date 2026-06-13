---
name: cost-breakdown
description: "Full COGS book (docs/cost-breakdown.md): fixed stack ~$182-294/mo ALL-IN; per-agent COGS (voice $30-40, textback $6-12, Executive $25-90); Sovereign ~$0 hard (all time); built from LIVE Hostinger+ElevenLabs pulls + verified 2026 unit rates"
metadata: 
  node_type: memory
  type: reference
  originSessionId: e5377b22-a7ba-4a0e-a66d-8ef60de63cac
---

Built 2026-06-12 at M's request. Doc: `docs/cost-breakdown.md` + PDF in Downloads. See [[sovereign-intelligence]], [[dbr-performance-offer]], [[website-business]].

**ACTUALS (live API pulls):** Hostinger account = $27/mo total (5 email plans $11.13/mo + 4 .COMs @ $20.19/yr + feerasta.ai $219.98/2yr = $9.17/mo): NO VPS on that account (hermes = Hetzner-range IPs, plan unknown, est $5-15/mo: pull invoice). ElevenLabs Creator $22/mo actual, 223,409 TTS chars (2% used), ~275 ConvAI min included; ConvAI overage $0.08/min, **LLM usage NOT bundled in minutes** (bills from credits).

**Fixed stack ~$182-294/mo all-in** (incl. Claude Max assumed $100-200, Lovable Pro $25, CF/Resend/Supabase all free tier). Stripe = cost of revenue: 2.9%+$0.30 +1.5% on Canadian cards charged by US account (~$66 on a $1,500 build).

**Key verified units (Jun 2026):** Twilio number $1.15/mo (US+CA); US SMS $0.0083/seg + carrier $0.0035-0.0045; CA SMS $0.0083 + carrier out $0.0064-0.0087 + **inbound carrier $0.015-0.017 (the missed line on 2-way campaigns)**; voice in $0.0085/min; A2P: brand $4.50 low-vol/$46 standard + $15 vetting + $1.50-10/mo. Lovable Pro 100 credits, top-up ~$0.30/credit. Resend free 3k/mo. Supabase free PAUSES after 1wk idle: go Pro $25 before live clients. .ai renewal ~$70-80/yr market (we pay $110/yr at Hostinger: savings available).

**Per-product hard COGS/mo:** Studio build $0-15 + 3-6hrs (care $2 + 0.5-1hr); Ascent $9-23 + 3-5hrs; Receptionist $30-40 (300min: $24 overage + $3-8 LLM + $1.15 number + $2.55 telephony); Text-back $6-12; Scheduler $12-25; Reviews $2-5; FAQ/Responder $2-8; Executive $25-90 + 2-4hrs/mo; Win-Back campaign ~$40-50 hard + 2-4hrs per 1,000 contacts (vs $2,000 typical revenue); Sovereign ≈ $0 hard, pure hours (Assessment 10-20h, S1 build 20-60h, client hardware billed at cost in THEIR account). Margins 90-99% cash everywhere.

**Open items:** confirm Claude Max tier; pull hermes VPS invoice; re-baseline voice-agent COGS after first real client month (watch ElevenLabs credit burn).
