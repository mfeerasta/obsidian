---
name: archie-sandbox-email
description: "How to hand Archie a file+email task — its tools run in a Docker sandbox; files go in the workspace mount, Gmail token must be synced into the sandbox home"
metadata: 
  node_type: memory
  type: reference
  originSessionId: 0b7d2d46-71b4-435e-9585-5da67e42f593
---

Archie (Hermes on hermes VPS) runs its **tools inside a Docker sandbox** (`nikolaik/python-nodejs`), NOT on the host. So host paths like `/home/hermes/pitch-emails/` are invisible to Archie — it refuses with "filesystem is a Docker container as root, /home/hermes does not exist." See [[tenant-agents-layer]], [[archie-website-funnel]], [[archie-health-2026-06]].

**Sandbox mounts** (`config.yaml` sandbox.backend: docker):
- host `/home/hermes/.hermes/sandboxes/docker/default/workspace` → container `/workspace`
- host `/home/hermes/.hermes/sandboxes/docker/default/home` → container `/root`

**To give Archie files for a task:** stage them under the host workspace dir and reference the container path. e.g. put PDFs at `…/sandboxes/docker/default/workspace/pitch-emails/` and tell Archie `/workspace/pitch-emails/…`. `chown -R hermes:hermes` the staged tree.

**Gmail/Google auth gotcha:** the gateway's fresh token lives at host `/home/hermes/.hermes/google_token.json`, but inside the sandbox the google tool reads `/root/.hermes/google_token.json` = host `…/sandboxes/docker/default/home/.hermes/google_token.json` — a SEPARATE, often-stale store. Symptom: `invalid_grant` even though the gateway's Gmail works. Fix: `cp /home/hermes/.hermes/google_token.json …/sandboxes/docker/default/home/.hermes/google_token.json` then re-run. (Don't scatter the token into guessed alt dirs — the classifier blocks that and only `.hermes/` is needed.)

**Trigger Archie one-shot (drafts/safe actions):** as the hermes user, `sudo -u hermes bash -lc "setsid hermes --yolo --skills <skill> -z \"<task>\" </dev/null >log 2>&1 &"`. `--yolo` disables approval gates (needs M's go-ahead; the classifier blocks it otherwise). Have it write a RESULT.txt to the workspace and poll that host path (ssh long ops drop — poll a file, don't hold the connection).

**Done 2026-06-10:** built 10 Bay Ridge pitch-email **drafts** (to bilal@feerasta.ai, subject = company + pitch hook, body + demo URL, 5 PDFs attached each: Pitch / Website Services Agreement / Invoice / Studio Plan / Ascent Plan — no demo sheet). Archie created them via this flow; verified 10/10 in Gmail with `to:bilal@feerasta.ai has:attachment`. Drafts only, not sent — M reviews/sends. Source packets: `~/Downloads/Feerasta Pitches/<Company>/`. See [[bilal-bayridge-demos]].
