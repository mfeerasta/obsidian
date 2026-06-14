---
name: ledger-app-demo
description: "Feerasta Ledger functional demo app (ledger-app/) built + deployed on Cloudflare Worker, zero-spend, stubbed at money-touching points"
metadata: 
  node_type: memory
  type: project
  originSessionId: e5377b22-a7ba-4a0e-a66d-8ef60de63cac
---

Built 2026-06-13 (M: "complete end product I can sell," weekend build, Cloudflare Worker page, build out everything). The marketing page existed ([[brand-architecture]]); this is the working software demo behind it.

**LIVE:** https://demo.feerasta.ai (custom domain on Worker `feerasta-ledger`; also feerasta-ledger.feerstone.workers.dev). Account 61d561ca9690ad9b59d9449181d90f12, deploys with same Workers token as main site. Linked from feerasta.ai/ledger ("See it live" hero + demo-band buttons → demo.feerasta.ai).

**PLAID bank feed (2026-06-14):** `plaid.js` does real server-side SANDBOX flow (/sandbox/public_token/create → exchange → transactions/sync), gated on Worker secrets PLAID_CLIENT_ID + PLAID_SECRET. No keys yet → returns labeled SIMULATION (8 txns) so the "Connect a bank → auto-categorized books" flow demos now (Money tab "Import bank transactions" button). engine.categorize() = rule-based categorizer (LLM in prod). **To go live (free, zero spend): M creates a Plaid account at dashboard.plaid.com, gives sandbox client_id+secret → I set them as `wrangler secret` → flips to real.** Sign convention: Plaid positive=outflow, we flip to negative=out.

**SCORECARD + BENCHMARK + HST (2026-06-14, "keep building"):** `engine.vendorScorecard(ds)` ranks vendors by overcharge $ (Invoices tab panel, "bring to price negotiation"). `engine.benchmark(ds)` vs per-vertical typical gross/net (BENCH map by tenant id) on Profit tab (apex: 65% gross above 55% typical, but 3% net below 8% = real insight). `engine.taxSetAside(ds, 0.13)` = Ontario HST set-aside estimate (collected − ITCs on non-payroll spend) on Overview, labeled estimate-not-filing. All in fullSummary.

**TREND CHART + RUNWAY + TRY-IT (2026-06-14, "keep building"):**
- `engine.history(ds)` = deterministic 6-month net/revenue series (prior months via REV_FACTORS × current, net via prior margin, last point = actual) → SVG bar chart on Profit tab (riverside shows 5 green months then June red, the anomaly dip). `engine.runway(ds)` = weeks of cash runway at this burn (weekly net = net/2); "Cash-positive" or "~N weeks" tile on Overview. Both in fullSummary.
- **Try-it tab** = the in-room closer: prospect types their own invoice lines (item / your price / billed / qty), client-side compare shows the overcharge caught live, nothing saved. Pure JS, zero backend.
- App now 13 tabs.

**6TH VERTICAL + EDGE PAGE + ROI PDF + AEO (2026-06-14, "build out all of these"):**
- 6th tenant **cedar (Cedar Dental)**: insurance-AR story ($10,050 outstanding / $8,700 overdue, slow insurers), 80.5% gross, 6.1× ROI, $2,100 X-ray sensor anomaly. 6 tenants total.
- **Branded ROI PDF export**: worker `/report?tenant=` serves a print-ready light-theme one-pager (headline + tiles + "what Ledger did" table + whole-business section); ROI tab button opens it. Samples generated: Feerasta-Ledger-ROI-Apex/Cedar.pdf in ~/Downloads/Claude Files/.
- **Feerasta Edge page** LIVE at feerasta.ai/edge (`portfolio-site/edge.html`, cloned Ledger shell): the hardware tier (invoice scanner / tablet POS / card reader / ID-age-verify+audit-log / desk phone for voice agent / on-prem Sovereign box). "We don't make hardware, we make it work." Wired into deploy.sh, sitemap, index footer, agents.json/agents.html/llms.txt.
- **AEO**: demo.feerasta.ai added to agents.json (top-level live_demo + on ledger service + contact notes), llms.txt, agents.html. Edge added as a service across all AEO surfaces.

**5 VERTICALS + ANOMALY + TREND (2026-06-14, "keep building"):** tenants now northline (c-store), riverbend (restaurant), apex (trades), **bloom (Lumiere Salon & Spa)**, **riverside (Riverside Auto Repair)**. New: `engine.anomalies(ds)` flags one-off/oversized spend (ONEOFF categories Equipment/Repairs/etc, or any non-Payroll/Rent/COGS expense ≥10% of revenue) → feeds Alerts (kind "anomaly") + digest; planted hooks: bloom $1,950 software migration, riverside $2,400 hoist repair (the reason riverside net is -$2,110). `engine.trend(ds)` = net/revenue vs ds.prior period → "▲/▼% vs last" on net tiles + OS. Riverside alerts screen = 8 flags / $9,824 at stake (overcharge+math+duplicate+anomaly+overdue). SAMPLES + deep-link updated for new tenants.

**FEERASTA OS + ROI + ONBOARDING + CRM (2026-06-14, "build out features"):**
- **Feerasta OS** = the unified one-screen moat: per-tenant `intelligence` (calls/missed-saved/bookings) + `ascent` (leads/reviews/GBP) added to data.js; engine.osSummary() merges Intelligence+Ascent+Ledger into one briefing + 3 cards (Front desk / Growth / Money). Default landing tab. /api/os.
- **ROI report** = engine.roiReport(ds): overcharges + duplicates blocked (hard $) + hours-saved×$28 (labor $) vs monthly fee → "X× back". ROI tab (printable) + /api/roi. Northline e.g. $1,180 value / 4.7× (the $928 dup bill dominates).
- **Onboarding** = in-app Setup wizard (3 steps: business → connect bank → first scan → live) + team checklist `docs/ledger-onboarding-checklist.md` (+PDF): free-week → go-live, compliance gate (A2P/data-residency/no-money-flow/AI-disclosure).
- **CRM** = Google Sheet "Feerasta Pipeline" in M's Drive (id 1eMec5hBamp7cF-MWFrXBeyRYJH0cP1-CEOz97LxETJo), seeded w/ Bay Ridge targets + Sophie's + Windsor batch. (Zapier sheets MCP is admin-restricted/halted; used Google_Drive create_file with text/csv → auto-converts to Sheet.)
- App nav now 12 tabs (Feerasta OS / Ledger / Invoices / Bills / Money / Profit / ROI / Receivables / Alerts / Connections / Ask / Setup).
- **Em-dash cleanup:** removed 43 em-dashes I'd wrongly used across ledger-app + docs + ledger.html (violated [[no-em-dashes]]); regenerated build-plan + sales-kit PDFs clean. Screenshots: Feerasta-OS.png, Feerasta-Ledger-ROI.png in ~/Downloads/Claude Files/.

**SALES KIT:** `docs/ledger-sales-kit.md` + `~/Downloads/Claude Files/Feerasta-Ledger-Sales-Kit.pdf` — per-vertical one-pagers (c-store/restaurant/trades, each tied to its demo tenant numbers), 90-sec demo script (lead with the invoice scan), objection handling, suggested pricing ladder (Lite ~$99 / Core ~$249 / Full ~$449 CAD, confirm before quoting), the close.

**MULTI-TENANT + ALL 6 MODULES (expanded 2026-06-14 on "build out all the features").** Code in `ledger-app/`:
- `data.js` — 3 demo tenants, each seeded so a DIFFERENT module is the hero: **northline** (c-store → invoice overcharges, thin 4% net), **riverbend** (restaurant → 68% food gross margin, 19.9% net), **apex** (trades → AR/collections: $10,220 outstanding / $7,600 overdue + a $3,305 Ferguson duplicate-bill catch). Each has price book, invoices (overcharges+math error), Plaid-style bank feed, receivables, bills (AP w/ a planted duplicate), connections. NO database on purpose: deploys with Workers-only token, zero spend.
- `engine.js` — pure fns over a per-tenant dataset: overcharge+math detection, cashflow/margin, **profit & loss statement**, **books/transactions view**, **bills/AP w/ duplicate + due-soon detection**, AR aging, **aggregated alerts feed** (overcharge/math/duplicate/overdue, human-in-loop status), connections, ask, digest, CASL/TCPA reminder.
- `worker.js` — tenant-aware (`?tenant=`); endpoints `/api/tenants|summary|overcharges|pnl|books|bills|receivables|alerts|connections|digest|ask|reminder|scan`.
- `public/index.html` — branded sidebar SPA, 9 tabs (Overview/Invoices/Bills/Money/Profit/Receivables/Alerts/Connections/Ask), tenant switcher, nav badges, deep-linking (`?tenant=apex#receivables`), per-tenant "scan sample invoice", reminder/schedule/dispute/dismiss/connect actions (stubbed).
- `schema.sql` (multi-tenant prod schema), `README.md`.

**Verified per tenant:** northline $34/period overcharges ($221 all-time), 39.2% gross, +$720 net; riverbend $146.50 overcharges, 68% gross, $5,440 net; apex $235 overcharges ($1,140 all-time), $10,220 AR / $7,600 overdue, $3,305 dup-bill saved. Screenshots in ~/Downloads/Claude Files/ (Feerasta-Ledger-Demo / -AR / -PnL / -Bills .png).

**Go-live gates (each needs M approval, all PAID/gated, none needed for the demo):** (1) vision OCR to replace stubbed `/api/scan` extraction (per-invoice cost); (2) A2P 10DLC + Twilio to actually send reminders; (3) Plaid production for live bank feed; (4) swap data.js for Supabase/D1 queries against schema.sql; (5) QBO/Xero/POS adapters. Stays OUT of the money flow (Stripe initiates, never holds funds) to dodge money-transmitter licensing; human-in-loop (no auto-dispute/auto-pay). See [[convenience-store-vertical]] (invoice-overcharge wedge), [[cost-breakdown]].

**Plan doc:** `docs/ledger-build-plan.md` + `~/Downloads/Claude Files/Feerasta-Ledger-Build-Plan.pdf` (full product plan: all client scenarios incl no-QBO via Plaid, 6 modules, synergies across the 5 lines, Feerasta Edge hardware tier, US+Canada legal guardrails, packaging tiers). Demo screenshot: `~/Downloads/Claude Files/Feerasta-Ledger-Demo.png`.
