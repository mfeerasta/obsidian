---
name: tenant-agents-layer
description: "Multi-tenant per-client agent layer (archie-tenant-agents/) — one isolated Hermes profile per client, the white-label instance-per-client product"
metadata: 
  node_type: memory
  type: project
  originSessionId: 0b7d2d46-71b4-435e-9585-5da67e42f593
---

Built + DEPLOYED 2026-06-08. The multi-tenant per-client agent layer that turns the Aria/Intelligence landing pages into a delivered, billable product (the OpenClaw white-label "instance per client" pattern). Lives in repo `archie-tenant-agents/`, DRY-RUN by default. Committed (4343100 miso, 9736f4c tenant-agents) + pushed to GitHub mfeerasta/feerstone main. DEPLOYED to hermes at `/home/hermes/.hermes/skills/tenant-agents/` (root, a+rX); migration applied to prod Supabase (growth.tenant_agents live, 17 cols); `tenant.py status` runs clean on the box as user hermes (registry empty, default gateway untouched). No live tenant provisioned yet (needs a signed client + the gateway-start spend).

**Architecture (rides Hermes v0.16 native primitives, nothing invented):**
- **Tenant = a Hermes `profile`** (`tenant-<slug>`). Native isolation: own config.yaml/.env/memories/sessions/gateway/number/model. Named profiles live at `$HERMES_HOME/profiles/<name>/`.
- **Profile targeting = `HERMES_PROFILE=<name>` env var** (confirmed in source; there is NO `-p` flag). Gateway is per-profile (`HERMES_PROFILE=tenant-x hermes gateway start`).
- **Template = `dist/`** = a profile distribution (`distribution.yaml` manifest: name/version/hermes_requires/env_requires/distribution_owned). Behavior shared; per-client facts ONLY in seeded memory `memories/tenant/knowledge.md`.
- **Provision = clone + overlay + seed + scrub:** `hermes profile create tenant-<slug> --clone --no-skills --description "..."` (reuses working default config), overlay dist SOUL.md + skills/receptionist + cron, seed knowledge from client facts, then SCRUB the cloned .env to a tenant allowlist (model + Twilio + TENANT_* only) so a tenant can't reach billing/banking/leads DB.

**Files:** `SKILL.md` (control-plane playbook), `scripts/tenant.py` (CLI: provision/seed/start/stop/restart/status/list/deprovision), `scripts/db.py` (asyncpg, lazy-import, reuses SUPABASE_DB_URL_RW; reads leads.clients, owns growth.tenant_agents), `migrations/0001-tenant-agents.sql`, `dist/{distribution.yaml,SOUL.md,skills/receptionist/SKILL.md,cron/jobs.json,knowledge.template.md}`.

**Flow:** funnel `bill.py` closes client → `tenant.py provision --client-id N --plan aria --number +1.. --mrr 199` (dry-run) → fill knowledge.md → `seed --live` → `start --live` (gateway = billed, approval-gated).

**Safety:** dry-run default; `--live` required; approval-gates (reuse funnel common.py) on gateway start + number purchase + deprovision; .env scrubbed to allowlist; no-fabrication baked into SOUL/skill; gateway OFF until explicit start. See [[archie-website-funnel]] (upstream funnel), [[brand-architecture]] (Aria = anonymous orphan, never names Feerasta), [[paid-key-permission]].

**Confirm on first LIVE provision:** that `profile create --clone` actually lands the profile at `$HERMES_HOME/profiles/tenant-<slug>/` (assumed from source). One-time check, like the only real unknown.

**Why:** OpenClaw/Hermes research showed per-client agent instances = $49-500/client/mo, 20 clients = $4-10k MRR. This is the delivery engine for that.
**How to apply:** deploy SKILL.md+scripts+dist to `/home/hermes/.hermes/skills/tenant-agents/` (root, a+rX) + run migration once → one command per signed client.
