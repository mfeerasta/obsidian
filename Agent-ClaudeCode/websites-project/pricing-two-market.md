---
name: pricing-two-market
description: Feerasta two-market pricing (US vs CA) + geo-switch on feerasta.ai; NY-first sales decision
metadata: 
  node_type: memory
  type: project
  originSessionId: 0b7d2d46-71b4-435e-9585-5da67e42f593
---

Set 2026-06-10 from NYC pricing research (Bilal's first NY sale). See [[bilal-bayridge-demos]], [[website-business]], [[brand-architecture]].

**Decision: US pricing raised, Canada unchanged.** $1,490 build was below NYC's freelancer floor (~$3,500) and signals "cheap" to a NYC owner. Kept the "affordable vs big-agency, month-to-month" wedge — only raised the floor.

| | US (USD, default) | Canada (CAD) |
|---|---|---|
| Studio build | from $1,500 | from $2,500 |
| Studio care | $100/mo | $150/mo |
| Studio premium | from $6,900 | from $4,900 |
| Ascent | $950/mo | $1,250/mo |
| Sovereign | NO public price (priced after Sovereignty Assessment) | same |
| Intelligence + AI Employee | NO public price (priced to the role after scoping) | same |

**Final (2026-06-10):** Studio US$1,500/CA$2,500 build + US$100/CA$150 care. Ascent flat US$950/CA$1,250/mo (single price, geo-switched). **Ascent = ALL-INCLUDED in the flat fee, NO revenue-share** (dropped 2026-06-10: local owners not pro buyers, keep simple; database reactivation folded into the $950, removed the separate rev-share pricing card + guarantee + FAQ on ascent.html and the Ascent plan PDFs). **Sovereign + Intelligence + AI Employee = NO price on the site** — assess the client's needs first, then quote (M's call). **BOUTIQUE = NO DISCOUNTS shown anywhere**; any lower price is negotiated in person, never on the site (no struck-through anchors, no "founding rate"). Logo = Feerasta lockup (assets/feerasta-logo.png) site-wide. Care plan default + scoped in docs/care-plan-scope.md. Bilal operator agreement: docs/operator-agreement-template.md. Pipeline now has competitor-features.ts (feature-gap) + template supports retail/auto/beauty/restaurant niches + financing/payment/featureBadge slots.

**Entity + payments (2026-06-10):** M is based in **Michigan** (not Pakistan as old CLAUDE.md says). Decision: form a **Michigan LLC** (home state, ~$50, single filing), NOT Wyoming/Delaware (double fees, no benefit) and NOT a C-corp. Foreign-qualify in NY when Bilal is actively closing there (NY publication req, budget $300-2k) and TX if a rep lands there. S-corp election later once net profit ~$60-80k. Sophie's agreement entity + governing law switched Wyoming→Michigan. **Stripe** = the card rail: live keys in vault, account submitted, card_payments still in review (transfers active). Payment flow = Stripe invoice/payment-link (card) + Zelle to payments@feerasta.ai; **ACH/direct-deposit removed from client docs**. Invoice = our own branded PDF (/tmp/invoice.html, matches the suite) carrying a Stripe "Pay by card" link, NOT Stripe's native template. STRIPE_SECRET_KEY set as feerasta-site Worker secret. Live catalog price IDs in vault (build/care/ascent).

**Geo mechanism (live on feerasta.ai studio + ascent):** prices tagged `data-us`/`data-ca`; inline script reads visitor country from Cloudflare's free `/cdn-cgi/trace` (loc=) — CA→CAD, everything else→USD. Bottom-right US$/CA$ toggle overrides + persists in localStorage across pages. US numbers are the no-JS default. Verified: CA edge auto-shows CAD, toggle swaps + persists. NOT applied to index (no prices) or sovereign/intelligence (enterprise).

**Bilal briefing (demo-first, quote only if asked):** US Studio build from $2,900, only pay after seeing it live; care $149/mo cancel anytime; Ascent growth system $897–$1,497/mo month-to-month vs big agencies $2,500–4,000 on 6-mo lock-in. Lead with "cancel anytime."

**First NY target = Sophie's Furniture** (storefront walk-in friendly, 124 reviews=most proven demand, big-ticket=clear website ROI, owner has budget). Demo upgraded with competitor-beating features (Snap apply CTA, contact form, same-day ribbon, payment badges, promo banner). Still NOT added (no real data, no fabrication): named brands, testimonials, real hours, product catalog w/ prices (= paid Phase 2 upsell).
