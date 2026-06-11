---
name: paid-key-permission
description: Ask M before using any paid per-use API key; infra keys (Cloudflare/Hostinger) need no permission
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 0b7d2d46-71b4-435e-9585-5da67e42f593
---

Always ask M's permission BEFORE using any paid, per-use API key — Anthropic, Gemini/Google AI, ElevenLabs, Perplexity, HeyGen, Firecrawl, OpenAI, etc. State what it's for + rough cost, then wait. Applies even mid-task and even if the key is already wired into a `.env`.

No permission needed for infra changes M already directed where there's no incremental cost: Cloudflare API (Workers/DNS/R2), Hostinger MCP, gh/GitHub, Supabase — those just execute the changes M asked for.

**Why:** these keys bill M per call/credit; M wants control over spend. Infra keys are flat-cost things he already owns.

**How to apply:** before a tool call that hits a paid key, pause and ask. Set in global CLAUDE.md "Paid API keys — ask before spending". Note: this session already used the Polymath Anthropic key (LLM offerings extraction) + the reused ElevenLabs key (video VO) before the rule was set — going forward, ask first. Relevant to [[website-business]] (ElevenLabs VO for prospect videos, Anthropic for brief extraction, Perplexity for research hooks).
