---
name: website-build-skills
description: 4 web-build skills installed + the website-generation playbook that folds them into our stack
metadata: 
  node_type: memory
  type: project
  originSessionId: 0b7d2d46-71b4-435e-9585-5da67e42f593
---

Jun 5 2026: analyzed M's "Wesbite & Marketing" skill pack + installed 4 skills to `~/.claude/skills/`: **website-intelligence**, **image-generator**, **3d-animation-creator**, **seo-strategy**. (The Canva + Notion "$10k AI websites / Antigravity" links couldn't be fetched — JS apps return empty shells; ask M to export if wanted.)

Synthesis lives at `Websites/docs/website-generation-playbook.md` — maps each skill onto our [[website-business]] core (`site-template` Astro multi-tenant + `lead-engine/src/brief-to-config.ts` demo-factory). Key takeaways:
- **website-intelligence** is the most valuable: its Phase-3 **competitive-analysis HTML report** = a cold-outreach SALES TOOL that pairs with our demo-first GTM ("I analyzed your top-5 competitors + already built you a site"). 6-phase: scrape client → score top-10 competitors (8 criteria) → PDF-ready report → build brief w/ HARD-STOP approval → premium GSAP scroll build → audit.
- **image-generator** (3-prompt scroll-stop video: hero-on-white / exploded / A→B transition) + **3d-animation-creator** (FFmpeg frames → scroll-driven canvas video site, Apple-style) = the PREMIUM tier ("different sites than ours" — product/launch/luxury). Save for Feerasta Studio's high-end offering, not local trades.
- **seo-strategy**: research-first, extract 20-40 LSI keywords from ranking competitors → gap analysis → rewrite. Fold into our programmatic service×city pages.
- Recurring pattern across all 4: deliver polished **HTML reports** as sales/client artifacts. Firecrawl is the scrape dependency (already wired). Maps to the **Feerasta Studio** (web) + **Feerasta Ascent** (marketing) divisions per [[brand-architecture]].

**Jun 5 — wired + Notion PDFs analyzed.** Built `lead-engine/src/competitive-report.ts` (`--slug <slug> --pdf`): real-brief → Places competitor pull → strength scoring → print-ready warm-paper competitive-analysis HTML+PDF in `briefs/<slug>/`. Tested on comfort-tek (works). This is the pre-pitch sales artifact. The 2 Notion "$10k AI Websites (AntiGravity)" PDFs analyzed → saved as `docs/antigravity-scrollytelling-prompt.md`: (a) the 3 image/video asset prompts, (b) the **AntiGravity Next.js 14 + Framer Motion + Canvas 120-frame scrollytelling system prompt** (premium scroll-stop sites, bg `#050505`), (c) the **UI/UX Pro Max 5-dimension framework** (Pattern/Style/Color/Type/Animation w/ exact palettes+fonts — luxury palette = stone `#1C1917`+gold `#CA8A04`+cream, Playfair+Montserrat+Cormorant; already have the `ui-ux-pro-max` skill). Build env in source = Google Antigravity/AI Studio + Vercel MCP deploy.
