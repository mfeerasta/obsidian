---
name: verifiable-info-only
description: "Client sites may state only verifiable info, sourced from the client's existing website + Google profile; no owner-confirmation bar, no assumed claims"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 0b7d2d46-71b4-435e-9585-5da67e42f593
---

When building a client website, a page may state ONLY information that is **verifiable from a public source**, specifically the client's own **existing website** (scan it if it exists) and their **Google Business profile** (scan it if it exists). Source every operational claim (hours, financing, delivery, services, payment methods, reviews, ratings) from those two scans.

**Why:** asserting unverified claims (e.g. we added "Snap Finance financing", "free delivery", "same-day" to Sophie's site from competitors) puts false statements on a real business's live site, a trust and liability problem, and breaks the demo-first promise that we never invent facts. See [[bilal-bayridge-demos]], [[website-business]].

**How to apply:**
- Build the fact set ONLY from: (1) scan their existing website if it exists, (2) scan their Google profile if it exists.
- If a business has NEITHER a website NOR a Google profile, then there is no verifiable source for those claims, so **omit those claims and the UI/features tied to them** (financing apply buttons, delivery promises, hours blocks, etc.) entirely. Do not include those tools.
- The bar is a **verifiable public source, not the owner's verbal say-so.** Owner confirmation alone does not license a claim; a checkable source does. (Owner can still supply info, but treat it as needing a verifiable basis before it goes on the public site.)
- Never use competitor-derived or assumed claims to "fill out" a site. A thinner, true site beats a fuller, fabricated one.
- This generalizes the existing pipeline rule that never fabricates and never claims "no website" without discovery.
