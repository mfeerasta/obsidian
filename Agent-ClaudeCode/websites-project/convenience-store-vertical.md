---
name: convenience-store-vertical
description: "C-store AI vertical eval: voice agent does NOT fit (walk-in, no phone pain). Real wedges = DSD invoice-overcharge detection + marketing/loyalty SMS for the ~90k underserved independents. Traps = checkout/fuel/shrink-vision/scheduling."
metadata: 
  node_type: memory
  type: project
  originSessionId: e5377b22-a7ba-4a0e-a66d-8ef60de63cac
---

Researched 2026-06-13 (M asked real-life c-store AI problems). Sourced from NACS, FDA, CDPH/SAMHSA, C-Store Dive/CSP/CSN trade press (vendor numbers flagged). See [[business-audit-build-priorities]], [[dbr-performance-offer]], [[demo-voice-lines]].

**Market frame:** 60% of US c-stores are single-store operators; 95,946 locations are 1-10 store "A-sized" ops (63%). NACS: ~90,000 single-store operators "don't have affordable access to digital solutions larger chains have (loyalty, apps, scan-data)." THAT is the underserved buyer.

**Our flagship voice/missed-call = POOR fit** (walk-in, ~zero inbound calls, no appointments, thin margins, owner at register). Confirmed. Don't send Bilal to bodegas with the voice pitch.

**Real problems, ranked by $ + sourced:**
- SPOILAGE ~$10,188/store/yr (NACS, single store) > merchandise shrink ~$2,868/yr. Spoilage is the bigger leak for independents.
- LABOR ~11% of sales; turnover 100-150%/yr, $3-5k per separation, churn in first 30-90 days.
- DSD INVOICES ~60-90/store/month; ~20% claimed to have errors (VENDOR claim, uncited). Manual receiving burden.
- AGE-VERIFICATION: FDA CMP escalates to $10k/violation, 5-in-36mo = No-Tobacco-Sale Order (existential); CA 2024 Synar 70.6% violation when ID not checked vs 2.4% when checked; Altria (Sept 2024) mandates carding ≤30 + ID-scan records or lose scan-data $.
- MARGIN: fuel 65% of sales but 38.8% of GP; in-store 35% of sales, 61.2% GP; foodservice highest margin. NACS msg: diversify off fuel. Card fees record $21.3B 2025.
- LOYALTY: members spend ~12% more; independents largely can't offer it. Delivery apps take 30-40% all-in AND the customer data (no names/emails).

**THE WEDGE (software-only, single-store-friendly, OUR stack):**
1. **DSD invoice-overcharge + price-change detection**: "snap the invoice → OCR+LLM extract → compare to price book → SMS the owner overcharges/price changes." No POS/DEX touch. Validated by a $17.99/mo incumbent (Pricebook app). Commodity OCR + LLM + Twilio.
2. **Marketing/retention layer for the ~90k underserved independents**: SMS win-back, loyalty/customer-data capture (recover identities lost to 30-40% delivery commissions), delivery-order consolidation. SMS ~98% open, cheap resellable tooling, AI-wrap it as managed service. Clearest lane.
3. (compliance third) **camera/tablet age-check + tamper-proof audit-LOG app** wrapping a cloud age API (Yoti ~$0.11/check): the audit trail is the sellable software; Altria mandate + Synar stat make the sale write itself.

**TRAPS (avoid):** autonomous checkout ($100-300k/store; Grabango died Oct 2024 after $70M, Amazon retreated); fuel price optimization (enterprise, rack feeds/forecourt controllers); shrink-vision (commoditized $75-200/mo by funded vendors, single-store loss too small to fund custom build, resell at most); scheduling (race to bottom, Connecteam free) — if touching labor, sell the retention/text-back layer around the 30-90-day churn window instead.

**Status:** vertical EVALUATED, not pursued. Park behind the verticals where the voice agent is an obvious yes (Bay Ridge locksmith/auto/clinic/restaurant). If pursued later, build the invoice-overcharge wedge first (cheapest to prove, clearest money story). No build started.
