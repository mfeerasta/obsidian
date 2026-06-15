---
name: pulse-product
description: "Feerasta Pulse = live busyness/occupancy product folded UNDER Edge (not a 7th line); sensor stack, pitch PDF, use cases"
metadata:
  type: project
  originSessionId: e5377b22-a7ba-4a0e-a66d-8ef60de63cac
---

Built 2026-06-14. **Feerasta Pulse** = live, verified busyness signal: anonymous occupancy sensor + POS fused into a 0-100 crowd score, a public "how busy are we" badge, a capacity/staffing dashboard, and retail conversion analytics. Privacy line: counts bodies, never a face, never records, clean under NYC biometric-identifier law.

**Positioning decision (M):** Pulse is NOT a separate business line. It is a **product within Edge**. Site is back to "Six lines, one standard." Pulse is surfaced as the "Crowd / occupancy sensor" device in Edge's device accordion; clicking it opens the full detail page `pulse.html` (canonical /pulse, still in sitemap, reachable via Edge + direct, not in nav/footer). Removed Pulse from nav/footer site-wide (129 links stripped) and from the homepage house grid + JSON-LD offers.

**Edge device section** was rebuilt as a click-to-expand accordion (`.dev-item` details/summary) where every device (invoice scanner, tablet POS, card reader, ID/age scanner, desk phone, on-prem AI box, crowd sensor) has a full description on click. Edge accent teal #6fae9f; Pulse page accent rose #c56b72.

**Sensor stack (prototype-ready, NOT deployed):** `portfolio-site/pulse-sensor/` = `host_counter.py` (Luxonis OAK-D overhead door counter: person detect + ObjectTracker on-device, host does line-crossing, POSTs only counts, no frames stored), `worker.js` (CF Worker: /ingest, /v/:venue.json, /badge.js embeddable pill; KV-backed; auto-learns per-venue max; mode busy vs empty), `wrangler.toml` (needs KV id + crowd.feerasta.ai route), README. Buy rec for the cam: **Luxonis OAK-D Lite ~$130** (own it, no SaaS, fits Edge); runner-up Density Waffle ($149 + $95/yr, turnkike but rented/cosmetic white-label).

**Use cases** (one sensor, two messages: "packed come now" vs "quiet, room now"): gym crowd meter (40% of members quit yearly, crowding a top cause), retail/c-store conversion rate (91% of clothing retailers track none; ~47% lift with footfall analytics), bars/restaurants verified-busy badge + live wait, hotels amenity occupancy, clinics live wait. Occupancy market $3.08B (2025) -> $7.54B (2032).

**Deliverable:** one-page pitch PDF `~/Downloads/Claude Files/Feerasta-Pulse-Pitch.pdf` (gym + retail + nightlife).

Pulse is reflected in AEO assets: llms.txt, agents.json (as `includes` under edge + service hint), agents.html. Also this session: Ascent generalized from trades-only to any local business + a use-cases section (HVAC/electrical/plumbing/salons/clinics/restaurants), fixed Ascent's stale FAQ price ($697-997 -> flat fee). See [[brand-architecture]], [[two-market-pricing]], [[agentic-shift-playbook]].
