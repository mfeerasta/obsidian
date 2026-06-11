---
name: stripe-demo-checkout
description: "Stripe pay-on-the-demo flow (buy button on each demo site), live/test accounts, catalog, the card_payments blocker, and the reusable Lovable components"
metadata: 
  node_type: memory
  type: project
  originSessionId: 0b7d2d46-71b4-435e-9585-5da67e42f593
---

Plan: put a "claim/buy this site" button **on each demo site we build** so a prospect who likes the demo can pay. The demo is the pitch; the close lives inside it. See [[website-business]], [[bilal-bayridge-demos]], [[voice-agent]].

**Mechanism (researched 2026-06-10):** Stripe **Buy Button** (`<script src="https://js.stripe.com/v3/buy-button.js">` + `<stripe-buy-button buy-button-id=... publishable-key=... client-reference-id=...>`, works in React/Lovable) OR simplest = a styled button linking to a **Payment Link** URL with `?client_reference_id=<company-slug>` for per-site attribution (arrives in the `checkout.session.completed` webhook). One link/button serves all 10 demos; each site passes its own slug. Layout = the template-marketplace pattern: a slim **sticky top "preview/buy" bar** + a **closing CTA before the footer** + "Secure checkout by Stripe" trust line. Checkout can charge the **$1,500 one-time + start the $100/mo** in one go (subscription mode + a one-time line item); care can start at launch via a trial.

**Stripe accounts (3, do not confuse):**
- Old **Feerstone sandbox** `acct_1Te5Pt…` = what the **Stripe MCP is connected to** (test). NOT the business account. Don't use the MCP for real billing.
- New **Tgpjg TEST** account (`sk_test_51Tgpjg…`, in vault) = the Feerasta personal/sole-prop account in test mode.
- New **TgpjX LIVE** account (`sk_live_51TgpjX…` / `pk_live_51TgpjX…`, in vault, holder Meer Feerasta) = REAL money. Live keys also set as CF Worker secret `STRIPE_SECRET_KEY` for feerasta-site.

**LIVE catalog (already created, USD):** Studio Build $1,500 one-time `price_1Tgq38LLEZyOsdqyOsOCXBcQ`; Studio Care $100/mo `price_1Tgq38LLEZyOsdqyWFeb5iw3`; Ascent $950/mo `price_1Tgq39LLEZyOsdqypLRRJWCe`.

**⛔ THE REAL BLOCKER (not "sandbox"):** live account `details_submitted=true, transfers=active`, but **`card_payments=INACTIVE` — Stripe is still reviewing the account.** Live Payment Links can't charge until that flips. Their review, not on us. The earlier "it's a sandbox" read was wrong; M does have live keys + live products. Creating a **live** payment-link object also trips the Claude classifier (real-money action) → needs M's explicit ok.

**TEST link built (for showing M, no real charge):** `https://buy.stripe.com/test_dRmbJ2gBa5Ly0BA0wKdZ600` (`plink_1Tgz9rLxjOnX4oMyjK1879Ib`; test prices `price_1Tgz9qLxjOnX4oMyUgFhDEzo` build + `price_1Tgz9qLxjOnX4oMyEsXh0kQT` care). Test card `4242 4242 4242 4242`. Script `/tmp/stripe_test_link.py` (reads test key from vault, creates catalog + link).

**Built on Sunset then REMOVED (2026-06-10):** Lovable project `9344d0b5-6527-4551-85d7-1fd6a8ca6c16` (sunset-supply-spark), commit `cf4f2c6`. Added `src/lib/demo-config.ts` (one `CHECKOUT_URL` const), `src/components/PreviewPayBar.tsx` (fixed top bar, site green + copper button), `src/components/ClaimSiteCTA.tsx` (before footer). M asked to **remove it for now** because the test checkout shows a Sandbox/test banner (can't use live yet). NOTE: the public sunset site never actually got it (the deploy/publish failed on a Lovable token expiry), so only the working copy had it. Components are **reusable**: to roll to the other 9, change `CHECKOUT_URL` + the business-name string per site.

**Custom checkout domain (2026-06-11):** `checkout.feerasta.ai` added as the Stripe custom checkout domain (so checkout runs on our domain, not stripe.com; "switch to this domain once added" checked). DNS on the feerasta.ai Cloudflare zone (`0e959a4fd92548c65126e0dd241f5836`), added via API (`/tmp/cf_dns.py`, token CLOUDFLARE_MIGRATION_API_TOKEN): `CNAME checkout -> hosted-checkout.stripecdn.com` (DNS-only / NOT proxied, else Stripe's CDN breaks) + `TXT _acme-challenge.checkout -> EllChOwTDRKkExJiGS18OB3tWtK2PY_Te8XB9mteTtM` (ttl 300). Stripe **verified both** ("DNS records updated and verified" + "added your custom domain"), now in the ~3-hour DNS-stability window (Stripe emails when done). Note: the TXT did NOT resolve via public dig (a child record under a CNAME name is occluded in normal DNS) but Stripe's verifier still read it fine — don't "fix" it by removing the CNAME.

**Go-live path (when card_payments is active):** (1) create the LIVE payment link ($1,500 build + $100/mo care; an Ascent-only variant for $950/mo) with M's ok, (2) swap the `CHECKOUT_URL` const test→live, (3) re-add the two components + redeploy each demo, (4) add a webhook on `checkout.session.completed` to notify M/Bilal + kick off go-live, (5) Customer Portal link for self-serve cancel ("cancel anytime").

**Stripe branding (Dashboard ONLY — API does not work for your own account).** Tried `POST /v1/accounts/{self}` `settings[branding]` → Stripe 403: *"You cannot use this method on your own account: you may only use it on connected accounts."* The Accounts API only edits Connect *connected* accounts; own-account branding is Dashboard-only. (Files API upload worked: icon `file_1TgzOsLLEZyOsdqylyNnGEWt`, logo `file_1TgzOtLLEZyOsdqyNB0zbQ0o` on the live acct, but they're unusable without the settings write.) So set it at `dashboard.stripe.com/settings/branding` (per-mode, do test + live): Icon = chip-F (`Websites/assets/favicon/favicon-512.png`), Logo = wordmark (`/tmp/flogo.png`), Brand color `#0b1018` navy, Accent `#b68b53` gold, business name Feerasta, support email sales@feerasta.ai. Applies to Checkout, Payment Links, receipts, invoices, Customer Portal.
