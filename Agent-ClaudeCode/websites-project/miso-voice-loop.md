---
name: miso-voice-loop
description: "Self-hosted Miso One TTS voice agent (Pipecat loop) scaffold, GPU-gated, fallback to ElevenLabs/Brian"
metadata: 
  node_type: memory
  type: project
  originSessionId: 0b7d2d46-71b4-435e-9585-5da67e42f593
---

The "most human" sales-call voice option: Miso One (Miso Labs, 8B open-weights emotive TTS, ~110ms, one-shot voice clone, NO hosted API). Because it's TTS-only, we self-host the full loop with Pipecat in `voice-agent/miso/`:

Twilio media WS -> faster-whisper STT (local GPU, free) -> nvidia NIM LLM (free, OpenAI-compatible, same key Archie uses) -> Miso One TTS (local GPU) -> back to Twilio. Zero per-minute cost on the GPU box.

Files: `gpu_probe.py` (run on host first, prints GO/NO-GO; needs 24GB+ VRAM), `setup.sh` (venv + CUDA torch + HF weights MisoLabs/MisoTTS), `prompt_loader.py` (reads the SHARED prompt `sales-agent-template-backup.json`, substitutes {{dynamic_vars}} — one brain across ElevenLabs/Retell/Miso), `miso_tts_service.py` (Pipecat TTSService; the ONLY file touching real weights — has a `TODO(miso-api)` block to reconcile import/call names once weights are on the box), `bot.py` (the pipeline), `server.py` (FastAPI: /outbound funnel trigger, /twiml, /ws).

Funnel wired: `place_sales_call.py --platform miso` POSTs to the Miso server's /outbound (env MISO_SERVER_URL); honesty guards (real competitor + real demo) unchanged.

**Status: PARKED (Jun 8 2026) — scaffold complete + compiles + security-hardened; no hardware to run it.** M said "save it for later." Tomorrow's Comfort-Tek call and all calls use [[voice-agent]] Brian + ElevenLabs (`--platform elevenlabs`). Not committed; not synced to hermes funnel copy.

**Hardware findings (the blocker):**
- M's GPU is a **Jetson Orin Nano Super, 7.4GB unified RAM** (ssh alias `jetson`, host `milo`, JetPack 6 / CUDA 12.6, arm64). Too small: 8B fp16 = ~16GB, won't fit. Nano can't host Miso 8B realtime.
- **DGX Spark** (128GB unified, ~273 GB/s bw) WOULD run it but M hasn't bought one; overkill + bandwidth-limited for this task (~$3-4k).
- Realtime 8B TTS is **bandwidth-bound**, so the cheap right buy = **used RTX 3090 24GB (~$700-900, 936 GB/s)** in a host PC, NOT the Spark. 16GB cards (4060Ti) too weak.
- Cheapest to validate before buying: **rent cloud RTX 3090 (~$0.30/hr, RunPod/Vast)** — M declined for now.

**Security note:** server.py is hardened (Jun 8 review): /outbound needs `Authorization: Bearer MISO_OUTBOUND_SECRET` (hmac.compare_digest, fails closed), /twiml validates X-Twilio-Signature, /ws accepts only single-use server-minted tokens, token charset-validated + quoteattr in TwiML. Funnel sends the bearer secret.

**Security fix applies regardless of Miso.** [[paid-key-permission]]: ElevenLabs is paid per-min — ask M before any live Miso/ElevenLabs spend.

**How to resume:** acquire 24GB+ box (rent 3090 or buy used) -> point setup.sh torch index at it (sbsa for arm, normal for x86) -> gpu_probe GO -> drop cloned voice WAV -> reconcile TODO(miso-api) -> start server -> A/B vs Brian before committing to buy.
