---
name: demo-voice-lines
description: "Two LIVE inbound demo voice lines (generic receptionist + restaurant) on ElevenLabs ConvAI: agent IDs, phone numbers, how they're wired. The 'hear it answer' proof for every pitch."
metadata: 
  node_type: memory
  type: reference
  originSessionId: e5377b22-a7ba-4a0e-a66d-8ef60de63cac
---

Built + wired live 2026-06-13 (M greenlit the paid build). Both answer INBOUND, Brian voice (nPczCjzI2devNBz1zQrb, stability 0.4), disclose they're AI in the first line (honest + EU AI Act Article 50 ready), end by pointing the caller to M's cell 248-828-6124. See [[voice-agent]], [[pitch-rework-ai-first]], [[sovereign-intelligence]], [[cost-breakdown]].

**LIVE DEMO LINES (call to hear them):**
| Line | Number | ElevenLabs phone_number_id | Agent name | Agent ID |
|---|---|---|---|---|
| Generic receptionist (adapts to any trade the caller names) | **+1 248-509-0888** | phnum_4701kchn31m6er1sfxx09wnp7jhb | Feerasta Demo Receptionist (inbound) | agent_0501kv0f42ace9hbgh1e7189ga60 |
| Restaurant receptionist (reservations/FAQ/multilingual) | **+1 249-523-1208** | phnum_0401kv0fc8dbeh295yxr980gkq83 | Feerasta Restaurant Receptionist (demo) | agent_8201kv0f6z5aecqb6htvvz8bk74s |

- 248 = metro Detroit area code; 249 = Windsor area code (the 249 number = the vault Twilio number +12495231208, account SID AC6875…, imported into ElevenLabs ConvAI 2026-06-13). The 248 number was already in ElevenLabs.
- Restaurant agent's 10 use cases + the design live in chat / to be doc'd; pending the booking-platform API research (OpenTable/Resy/TheFork/SevenRooms/Mozrest) to decide live-availability vs capture-and-hand-to-staff.

**How wiring works (the ElevenLabs MCP can't do this, API only):** the MCP only exposes create_agent / list / make_outbound_call: **no inbound-assignment tool**. To attach an agent to a number or import a Twilio number, use the REST API with the xi-api-key (in `~/.claude.json` MCP config; grepping it is classifier-gated, M must authorize each time):
- Import Twilio number: `POST https://api.elevenlabs.io/v1/convai/phone-numbers` body `{phone_number, label, provider:"twilio", sid, token}` → returns phone_number_id.
- Assign agent: `PATCH /v1/convai/phone-numbers/{phone_number_id}` body `{"agent_id":"..."}`.
- Other existing agents on this ElevenLabs account: Vape Buyer Inquiry (agent_5401ktt6gk3weg79tkg0ajkevh1t), Feerasta Local Website Sales outbound (agent_0201kt8bvrhsf1j94nhpmy775y7k), Archie M's Assistant (agent_8801kspwz5e3fxgr3h4jf243ze49), Range Rover Service Inquiry (agent_7301kchhjnzcfc8thzme7nxjevj4).

**Cost:** numbers already paid in Twilio (~$1.15/mo each); per call = Twilio ~$0.0085/min + ElevenLabs ConvAI minutes (Creator plan ~275/mo included, then $0.08/min) + small LLM tokens. Demo volume = pennies. **TODO:** test both lines (confirm voice/flow), then add the demo number to the Windsor email drafts + Bilal's NY kits ("hear it yourself: call …"). pt-PT restaurant variant when Portugal launches.
