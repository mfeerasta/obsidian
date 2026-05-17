---
name: utilities-and-bill-refs
description: Utility account/meter references (LESCO electricity, SNGPL gas, WASA water, etc.) for MF properties and businesses. Source of truth for bill-fetching crons.
metadata:
  type: reference
---

# Utilities and Bill References

Authoritative list of utility account numbers, meter IDs, and recurring bill references across M's properties and businesses. Used by Hermes cron jobs (`monthly_lesco_bills.py`, future SNGPL/WASA scripts) to fetch bills.

## LESCO (electricity, Lahore Electric Supply Company)

Bill fetch endpoint: `https://www.lesco.gov.pk/Modules/CustomerBill/CheckBilling.asp?refno=<14-digit-ref>`

| Property / Use | Reference No (14-digit) | Customer ID | Tariff | Notes |
|---|---|---|---|---|
| RFB (Rupafab) | `24112223003600` | `3001351` | B2b(12)T | Rupafab Limited factory, Raiwind Road LHR, Pajian feeder, Jia Baga sub-div, Raiwind div. Connection date 06 JUL 95. NTN 0298221-8, GST 1401511100164. Conn load 451. Account holder: Amir ud Din Jaufar Ali / M/s Rupa Fab. |
| ZP - Net Meter | `24112520008205` | `11328825` | A-1b(03)T | ZP solar net-metering, Zaman Park feeder, G.O.R sub-div, Civil Line div. Connection date 12 AUG 25. DG capacity 19.89 kW. Account holder: Amir Feerasta s/o Jaffar Ali Feerasta, 1 Zaman Park Lahore. |
| ZP - Old Meter | `06112520508500` | `3176712` | A-1b(03)T | ZP conventional meter (pre net-meter), Shadab Colony feeder, G.O.R sub-div, Civil Line div. Connection date 08 JUN 98. Account holder: Malik Sultana J Firshta w/o Jafar Ali Firshta, 1-Zaman Park Lahore. Mobile 923056289028. |

To add a new meter: append a row and update `~/.hermes/scripts/monthly_lesco_bills.py` LESCO_REFS list.


## Latest LESCO bills snapshot — Apr 2026 (fetched 2026-05-17 via Playwright)

| Account | Bill Month | Units (kWh) | Payable Within | Due Date | After Due | Status |
|---|---|---|---|---|---|---|
| RFB (Rupafab) | Apr 26 | 1,920 | PKR 136,100 | 21 May 26 | 140,487 → 144,874 | unpaid |
| ZP Net Meter | Apr 26 | 2,300 (export 2,060 / import 1,820+480 peak) | PKR 34,494 | 21 May 26 | 35,864 → 37,234 | unpaid |
| ZP Old Meter | Apr 26 | 12 | PKR 11,782 | 29 Apr 26 | 12,280 → 12,778 | PAID 23-Apr-26 |

Total currently outstanding: **PKR 170,594** (RFB + ZP Net Meter).

Update this snapshot by re-running the cron job (will auto-populate via Playwright once  is wired to drive browser instead of HTTP-only).

## SNGPL (gas, Sui Northern Gas Pipelines)

(none captured yet — add as discovered)

## WASA / WASA-PHA (water, Lahore)

(none captured yet)

## PTCL / Internet / Telco

(none captured yet)

## Banking

See `[[reference_sbl_profit_credits]]` for SBL profit credit pattern.

## How Hermes uses this

1. `~/.hermes/scripts/monthly_lesco_bills.py` reads the LESCO table above, fetches current bill HTML per ref, parses outstanding amount + due date, prints summary to stdout.
2. Cron job `f06650014158` (profile A, schedule `0 9 1 * *`) runs the script monthly, delivers stdout to origin (default = WhatsApp M / 923018444356).
3. To add a new utility category: new section here, new script under `~/.hermes/scripts/`, new cron via `hermes cron create '<sched>' --script <name>.py --no-agent --deliver <target>`.

## How to update

Edit this file directly. Both profiles see it via shared `memories/` symlink. Hermes agent has read-only access at prompt-time.
