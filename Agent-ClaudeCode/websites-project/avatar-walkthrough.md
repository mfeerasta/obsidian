---
name: avatar-walkthrough
description: Plan to deliver remote website walkthroughs via an AI avatar of M (HeyGen)
metadata: 
  node_type: memory
  type: project
  originSessionId: 0b7d2d46-71b4-435e-9585-5da67e42f593
---

For prospects M can't visit (Toronto + anywhere outside Windsor-Detroit) who want to "pop in on a Zoom" to see their pre-built demo site. Plan PDF: `~/Desktop/feerasta-avatar-walkthrough-plan.pdf`; source `portfolio-site/avatar-walkthrough-plan.html` (committed on main 2026-06-08).

**Tool reality (researched 2026-06-08):** **HeyGen LiveAvatar** = real-time WebRTC avatar, LLM-driven, and in 2026 it can **join a Zoom/Teams call as a participant** → the live use case. (Interactive Avatar sunset Mar 31 2026 → LiveAvatar.) **Higgsfield = pre-rendered gen-video ONLY (Seedance/InfiniteTalk), NO real-time** → good for async video, useless for live. **Tavus** = purpose-built live conversational-video alt (backup). 

**Staged plan:** Phase 1 = **async personalized walkthrough video** per prospect (HeyGen Video API digital twin $1-5/min, or Higgsfield credits) — voice agent texts the link; cheap, scalable, ~80% of value / ~20% of build. Phase 2 = **live HeyGen LiveAvatar** joins a branded web room/Zoom, screen-shares the site, answers Q&A (disclosed as AI). Phase 3 = **real M on Zoom for big clients** (booking routes by deal size). Reuses the funnel: same prospect dynamic vars (business/demo_url/reviews/competitor) = the avatar's brain; pre-built demo sites = its content; the [[voice-agent]] sales prompt = its script.

**Costs:** HeyGen Creator $29 / Pro $99 / Business $149+$20/seat; **LiveAvatar slot $49/mo** (Business+); async render $1-5/min. Phase 1 ≈ $29-99/mo + per-video; Phase 2 adds ≈ $149+$49/mo base. Start Phase 1; take Phase 2 base only when live calls are requested.

**Risks:** disclose it's M's AI (honesty + legal, same as calls); uncanny-valley/quality gate before any prospect sees it; live latency tuning; Phase 2 screen-share is the hard part (use a HeyGen-hosted web room, not literal Zoom virtual-cam).

**M's decision 2026-06-08: do NOT pay for the avatar yet — wait for a real remote-walkthrough need, then pay. Pre-build everything so activation = pay → drop key → flip on.** Done: repo **`avatar/`** package (committed on main): `walkthrough-script.md` (the avatar brain — parameterized narration, professional register, AI-disclosed, reuses voice-agent {{vars}}), `render_walkthrough.py` (orchestrator: `--mode video|live|higgsfield`, DRY-RUN with a readiness check showing missing keys + account-side reqs; real render call STUBBED for activation), `README.md` (pay-and-go checklist + HeyGen MCP activation).

**Official HeyGen MCP exists** (heygen.com/model-context-protocol): two modes — **Remote** (`claude mcp add --transport http heygen https://mcp.heygen.com`, OAuth, no key, uses plan credits — easiest) or **Local** (uv + `HEYGEN_API_KEY`). For Archie: `mcp_servers.heygen` env-map pattern. **Do NOT add until M has a paid HeyGen plan** (MCP spends plan credits). HeyGen key steps: app.heygen.com → paid plan (Free has no API) → Settings → API → Create New Token.

**To ACTIVATE when a client needs it:** Phase 1 video = HeyGen Creator/Pro OR Higgsfield (connected) + a photo/training-video of M + set `HEYGEN_*`/`HIGGSFIELD_*` env → `render_walkthrough.py --mode video|higgsfield --live-render`. Phase 2 live = HeyGen Business $149 + LiveAvatar slot $49/mo + token → `--mode live`. Big clients → real M, not the avatar. Always disclose it's M's AI.
