---
name: restaurant-availability-architecture
description: "How the restaurant voice agent answers 'do you have a 5pm for 2?' when OpenTable/TheFork/Resy hold the book. 5 ranked options; M leaning option 2 (shared Google Calendar as single source of truth)."
metadata: 
  node_type: memory
  type: project
  originSessionId: e5377b22-a7ba-4a0e-a66d-8ef60de63cac
---

Designed 2026-06-13. The bottleneck: source-of-truth availability lives inside the walled booking platform (OpenTable/TheFork/Resy, no clean API). See [[demo-voice-lines]], [[portugal-feasibility]].

**Core reframe:** availability is a CALCULATION, not a lookup. Available 5pm 2-tops = (2-tops the room seats at 5pm, configured once at setup) minus (2-tops already booked). The agent needs the second number without double-booking. Five ways, best→worst:

1. **Allocation / hold-back (zero integration, ships today):** carve the room: platform manages most inventory, agent owns a dedicated pool (e.g. 3 tables/slot). Within its pool the agent gives a hard yes/no, ZERO double-book risk (nothing else touches those tables). Tradeoff: may say "full" when the platform pool had space. How phone-vs-online splits already work.
2. **Shared Google Calendar as single source of truth (M's pick; one real API, full-room awareness):** platform pushes confirmed reservations into one Google Calendar (native or Zapier bridge), agent reads+writes the same calendar, computes availability live across the whole room, writes its bookings back so the platform's next customer sees the slot gone. Uses Google Calendar API (open/free/solid), no platform API. Variable: how cleanly each platform exports to a calendar (OpenTable native GCal sync is NOT standard → usually Zapier/email-parse glue → adds fragility + setup time; verify per platform per client).
3. **Authorized dashboard read (works, fragile):** client consents, we log into THEIR OpenTable-for-Restaurants account via computer-use/RPA, read the live floor grid. Legit (authorized) but dashboards change + bot-protected.
4. **Platform's real API (upgrade tier):** SevenRooms (open, voice-AI vendors already on it), Mozrest (50+ systems, one integration), OpenTable Sync (SOC-2 + partner approval), TheFork (Lisbon's dominant book, email-gated). Full real-time. The destination.
5. **Tentative hold + confirm-by-text (universal fallback, no integration):** "I've got you tentatively at 5 for two, confirmation text in a few minutes." Host stand confirms against the real book. No double-book, beats voicemail, works for ANY restaurant incl. Resy/Tock where handoff is the only legal path.

**DO NOT:** scrape OpenTable/Resy to fake real-time access. ToS-violating, bot-protected, one C&D from killing the product.

**Recommended build path:** start every restaurant on #1 (allocation) + #5 (tentative-confirm overflow) = honest yes/no day one, no platform dependency. Add #2 (shared calendar) as the standard upgrade for full-room awareness. Add #4 for clients on SevenRooms/Mozrest/TheFork. Match each client to whatever book they run.
