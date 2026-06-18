---
name: bespoke-and-advisory-law
description: "Feerasta Bespoke (7th line, custom AI/software, LIVE on site) + the consulting/financial-advisory licensing rule that guards it"
metadata: 
  node_type: memory
  type: project
  originSessionId: e5377b22-a7ba-4a0e-a66d-8ef60de63cac
---

Built + pushed live 2026-06-17. **Feerasta Bespoke = the 7th line** (`portfolio-site/bespoke.html`, bronze accent rgb(184,138,108)): custom AI & software for a client's specific problem when nothing off-the-shelf fits, custom agents / automation / integrations / internal tools / RAG / private on-prem AI. Process = **Blueprint** (paid fixed-scope discovery, credited to build) then **Build** (fixed price) then optional **Run** (retainer). Pricing geo: blueprint from $500 / C$650 / €450; build "scoped per project"; run "monthly retainer". Wired site-wide: nav + footer Divisions across pages (script-inserted after Edge), homepage grid card + "Six→Seven lines", a Bespoke linerow on /pricing, AEO (agents.json "bespoke" service + index.html JSON-LD brand/makesOffer, llms.txt). deploy.sh includes bespoke.html. (Edge HTML cache lingers ~minutes after deploy; revalidates on max-age=0.)

**Consulting/advisory licensing rule (docs/consulting-advisory-law.md + PDF), the guardrail:** building software/AI + general business/ops/tech consulting = **NO licence** in US/CA/PT. **Regulated (need credential):** investment/financial advice (US: RIA + Series 65; CA: provincial securities reg CSA/CIRO + protected titles "Financial Planner/Advisor" in ON/QC; PT: CMVM/MiFID II), securities/insurance, legal advice (bar/Ordem dos Advogados), official accounting/audit/tax filing (CPA/EA/OCC-Contabilista Certificado). **So our money/law-adjacent products are TOOLS not ADVICE.** Bespoke page carries the line: "We build the software and AI; we are not your lawyer, accountant, or financial adviser; regulated advice stays with your licensed professionals." Same posture as Ledger ("works alongside your accountant, never files taxes"). Keep this line on any money/legal-touching build.

Related: [[feerasta-listings]], [[whatsapp-bridge]], [[brand-architecture]], [[verifiable-info-only]].
