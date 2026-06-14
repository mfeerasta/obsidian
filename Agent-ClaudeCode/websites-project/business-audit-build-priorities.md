---
name: business-audit-build-priorities
description: "Full business audit + the 3 research-backed ops build priorities (ROI report, QA/monitoring loop, templated 48h onboarding) + Bay Ridge voice-agent target list for Bilal. docs/business-audit-build-priorities.md"
metadata: 
  node_type: memory
  type: project
  originSessionId: e5377b22-a7ba-4a0e-a66d-8ef60de63cac
---

Built 2026-06-13 (M: audit all areas + find Bay Ridge voice-ideal businesses since the website pitch died on Bilal). Doc: `docs/business-audit-build-priorities.md` + PDF. See [[demo-voice-lines]], [[restaurant-availability-architecture]], [[pitch-rework-ai-first]], [[cost-breakdown]], [[bilal-bayridge-demos]].

**Diagnosis:** materials/strategy far ahead of operations, and research says that's backwards: 43% of SMB clients lost in first 90 days, **42% of cancellations = "no visible ROI."** We have nothing that proves ROI to a client or catches an agent misbehaving. Sell now; build the retention layer right behind the first win.

**3 RESEARCH-BACKED BUILD PRIORITIES (in order):**
1. **Monthly ROI report as a product** (off agent call logs + growth schema): 6-8 KPIs + "X calls handled, you'd have spent $Y on staff" + 30-60-90 cadence (day-14 report, weekly→monthly check-ins, quarterly review w/ annual-contract offer). The #1 anti-churn artifact; we don't have it.
2. **Our own QA/monitoring loop** (don't trust ElevenLabs to alert): auto-score 100% of calls cheap classifier, daily AUDIO review (not just transcripts), alert on rising failure clusters, human approval gate before any prompt change. "Set-and-forget" = the deadliest mistake (real agent degraded silently 4 months). Watchdog = uptime; this = quality. Cap live agents until built.
3. **Templated 48h onboarding + parallel-run** (make the promise real + cheap = the margin): KB from REAL call data not just website, calendar/CRM wiring, escalation flows, QA test battery, run agent in OVERFLOW/parallel before main-line cutover (phased rollout 3x more success than big-bang), gate go-live on tests.

Smaller do-anyway: register A2P 10DLC (blocks all live SMS), Supabase Pro before live client (free tier pauses after 1wk idle), enable tenant watchdog cron, finish Stripe publish/branding, build a pipeline/CRM tracker (no prospect tracking exists today).

**BUILT 2026-06-13: `~/Downloads/Claude Files/Bay Ridge Voice Pitches/`** (8 PDFs, dark theme): 5 voice-pitch one-pagers (Verrazano Locksmith, Centers Urgent Care, Bay Ridge Auto Care, Fifth Avenue Dental, Tanoreen) each w/ verified pain + tailored use cases + demo-line CTA + Bilal contact + "from $399/mo, free week first"; **Monthly ROI Report SAMPLE + blank TEMPLATE** (the #1 anti-churn artifact: statband + 6 KPIs + "what it was worth" $ chart [jobs × avg job value vs fee] + bottom-line "$2,400 human receptionist who goes home at five" + "what we tuned" + 30-60-90 cadence note); Bilal Voice Door Card (90-sec script: "hear something for ten seconds?" → dial demo on speaker → free week → $399 cancel-anytime + objection map + best-doors order). Generator: tmp/voice_pitches.py off the theme module. ROI report still needs the BUILD (generate from real agent call logs + growth schema) to be a live product; this is the design.

**BAY RIDGE VOICE TARGETS (for Bilal: voice agent = easier sell than the dead website pitch).** Territory dense + workable (86th St 100+ businesses, 3rd Ave restaurant/clinic/salon spine, 5th Ave dental/PT/CPA). TOP 5 efficiency wins: Verrazano Locksmith (24/7, 2am lockout), Centers Urgent Care 3rd Ave (~100min waits), Bay Ridge Auto Care/J&D (owner under a car), Fifth Avenue Dental (reviews already complain of dropped appts), Tanoreen (1,100+ reviews, 20-min phone-hold reservations). Then: Vesuvio/Peppino's/Cebu restaurants, D&J Nail/MOKO/Bay Ridge Barber, FYZICAL/PT of the City, Jacoby&Meyers + MEI CPA, Animal Clinic of Bay Ridge. **Positioning rule:** phone-only shops (locksmith/auto/urgent-care/CPA) = "the agent IS your front desk" (strongest); businesses with Resy/Booksy = "after-hours + overflow channel, not a replacement." Verify address/phone on own site + open status before calling (some from aggregator snippets; one nearby urgent care shows closed). Lead with the live demo line.
