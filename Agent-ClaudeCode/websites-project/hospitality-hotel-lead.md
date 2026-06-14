---
name: hospitality-hotel-lead
description: "Hospitality vertical added + warm hotel lead (Comfort Inn & Suites Windsor, M's sister works there); who to pitch"
metadata: 
  node_type: memory
  type: project
  originSessionId: e5377b22-a7ba-4a0e-a66d-8ef60de63cac
---

Added 2026-06-14. M's **sister works at the Comfort Inn & Suites in Windsor, ON, near the Ambassador Bridge**; she says they get a lot of calls. This is a warm voice-agent (Intelligence) lead.

**Why hotels fit the voice agent (esp. border hotels):** front desk can't answer phone + check in a lobby at once; AI answers all calls in parallel (no busy signal), 24/7/after-hours night coverage, takes/modifies reservations, captures DIRECT bookings (saves the 15-30% OTA commission to Expedia/Booking), answers border questions (parking, breakfast, distance to bridge/tunnel), multilingual (French for Canada), transfers to staff. Caveats: needs PMS/booking-engine integration for live availability (else capture-and-confirm); Choice Hotels franchise brand rules may apply.

**WHO TO PITCH:** the **General Manager** (decision-maker at a franchised limited-service hotel) and/or the **franchise owner** (most Comfort Inns are independently owned; the owner/GM buys local services, NOT Choice corporate). Front-desk/ops manager = internal champion, not budget. Action: ask sister who the GM is + whether independently owned and by whom; warm-intro the GM.

**LIVE DEMO LINE (2026-06-14):** call **+1 249-523-1208** to hear the hotel front-desk agent (ElevenLabs ConvAI, agent_1501kv3pw4rjfbq9dsbsf33n4z7h, "Comfort Inn & Suites Ambassador Bridge (front desk demo)", Brian voice, scripted with VERIFIED property facts from Google/listings/Choice: 2330 Huron Church Rd N9E3S6, front desk 519-972-1100, check-in 3PM / check-out 11AM, complimentary hot breakfast weekdays 6:30-9:30 / weekends 7-10, free parking + wifi, fitness centre, meeting space, 24h business centre, laundry, patio BBQ seasonal, 125 non-smoking rooms / 4 suite types / main-floor walkout, smoke-free. Pets: 1 dog =25lb in a standard room +CA$60/night, no cats. **POOL CURRENTLY NOT AVAILABLE, agent says pool temporarily unavailable, never says it's open (M flagged this).** Defers exact rates to desk. Updated via ElevenLabs REST PATCH /v1/convai/agents/{id}. **This reused the restaurant demo's 249 number, so the restaurant demo line is now OFFLINE** (re-provision a new number if the restaurant demo is needed again). Reassigned via ElevenLabs REST PATCH /v1/convai/phone-numbers (MCP only lists). Also a redundant "Bridgeview Inn" demo agent agent_7501kv3pjtrdfj3rna2qzg4q7eff exists (can delete). Real hotel: operated by Sunray Group.

**Deliverables built:** one-page hotel pitch `docs/hotel-pitch-comfort-inn.md` + `~/Downloads/Claude Files/Feerasta-Hotel-Pitch-ComfortInn.pdf` (leave-behind for the GM). **Hospitality** added as the 10th resources vertical (5 articles, article-hospitality-*) on feerasta.ai/resources + homepage industries strip. See [[demo-voice-lines]] (live demo numbers to play), [[bilal-bayridge-demos]], [[business-audit-build-priorities]].

**Site state note (2026-06-14):** feerasta.ai resources hub now = 80 articles across 10 verticals (cstore/restaurant/trades/salon/auto/dental/medical/legal/fitness/hospitality), central /faq, rich 3-col footer site-wide, per-page accent-colored icons, geo-gated US/CA pricing (server-side worker), expanded detail-rich homepage. Ledger demo at demo.feerasta.ai.
