---
name: maps-places-api
description: "Google Places lead pulls: the google-maps MCP is bound to a DISABLED project; use the websitecreator-498218 key (in vault) via direct curl instead"
metadata:
  type: reference
  originSessionId: e5377b22-a7ba-4a0e-a66d-8ef60de63cac
---

For Bay Ridge / local-business lead pulls (ratings, reviews, phone, website-gap):

- The connected **google-maps MCP** uses an API key bound to Google Cloud project **505853880585**, where Places API (New) is **disabled** (403 PERMISSION_DENIED). The MCP cannot be pointed at another project from the session, so it fails.
- **Workaround that works:** call Places API (New) directly via curl with M's key for project **websitecreator-498218** (saved in `~/Desktop/feerasta-credentials.md`, added 2026-06-14). This is a PAID per-call key, M approved its use for lead pulls.
- Endpoint: `POST https://places.googleapis.com/v1/places:searchText`, headers `X-Goog-Api-Key`, `X-Goog-FieldMask: places.displayName,places.rating,places.userRatingCount,places.nationalPhoneNumber,places.websiteUri,places.formattedAddress`; body textQuery + locationBias circle (Bay Ridge center 40.6264,-74.0299). Ask M before large runs (per-call cost).
- Strongest lighthouse signal = high rating + many reviews + NO websiteUri + listed phone (loved, reachable only by phone, invisible in search). Bay Ridge pull (2026-06-14) top targets: 75th Street Auto Center (4.8/164/no site), 3rd Ave Auto (4.7/185/no site), Sally Beauty Nail Spa (4.7/330/no site), Tiba Dental (4.7/731, no-show wedge). Full ranked list + pre-filled audits in ~/Downloads/Claude Files/. See [[bilal-bayridge-demos]], [[verifiable-info-only]], [[paid-key-permission]].
