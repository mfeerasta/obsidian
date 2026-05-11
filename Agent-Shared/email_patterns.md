---
name: Rupafab email routing patterns
description: Per-category sender / recipient / CC patterns + subject prefix conventions. Used by Hermes to draft outbound mail mirroring company conventions.
type: reference
---

# Rupafab email routing — per category

Hermes uses these patterns when drafting replies or sending new mail in any category. Pull To/Cc/subject-prefix from the category here, then run through `hermes_mailer.send()` (auto-CCs meerfeerasta@gmail.com always).

## Key people / mailboxes

| Address | Person / Role |
|---|---|
| asifh@rupafab.com | Asif Hashmi — Accounts Manager (primary author) |
| accounts.payable@rupafab.com | Ashar Sharif — AP, daily approvals |
| mfeerasta@rupafab.com | Meer (you) — biz address |
| afeerasta@earthlink.net | Amir (Dad) — primary personal |
| afeerasta@hhhc.com | Amir secondary (medical) |
| afeerastapk@gmail.com | Amir PK Gmail |
| meerfeerasta@gmail.com | Meer personal Gmail (always auto-CC) |
| accounts@rupafab.com | Rupafab accounts mailbox (group) |
| srzaidi5@gmail.com | Senior consultant (FBR / GST matters) |
| uzain0807@gmail.com | Zain — FBR consultant |
| mlawakeel@gmail.com / mustafalawassociates1@gmail.com | Mustafa Law Associates — litigation |
| apaamorais@gmail.com / carla.lencastre@gmail.com | Portugal tax representatives |
| mianasghar124@gmail.com | PK property/excise consultant |
| amfeerasta@gmail.com / kmfeerasta@gmail.com | Family Gmail aliases |
| chishti.ghulam@soneribank.com / arslan.shehzad@soneribank.com | Soneri Bank relationship officers |

## Category routing matrix

### FBR
- **Drafter**: Asif (asifh@rupafab.com) — 31/50
- **TO**: srzaidi5@gmail.com (consultant) + mfeerasta@rupafab.com + asifh@ + uzain0807@gmail.com + afeerasta@earthlink.net
- **CC**: accounts@rupafab.com (always)
- **Subject prefix**: `Rupafab Ltd.` or `RFB-ACCT-`

### SECP
- **Drafter**: Asif or Meer
- **TO**: mfeerasta@rupafab.com + afeerasta@earthlink.net + afeerastapk@gmail.com (Amir's PK Gmail)
- **CC**: accounts@rupafab.com
- **Subject prefix**: `RFB-ACCT-`

### PESSI / WWF
- **Drafter**: Asif or Ashar (accounts.payable)
- **TO**: mfeerasta@rupafab.com primary
- **CC**: afeerasta@earthlink.net (always Amir on labor disputes)
- **Subject prefix**: `Rupafab Ltd:` or `RFB-`

### EOBI
- **Drafter**: Ashar (AP)
- **TO**: mfeerasta@rupafab.com
- **CC**: afeerasta@earthlink.net + asifh@

### PK Property Tax (Excise & Taxation)
- **Drafter**: Ashar (AP), Amir, or Asif
- **TO**: meerfeerasta@gmail.com (personal) + afeerasta@earthlink.net + mfeerasta@rupafab.com
- **CC**: asifh@rupafab.com
- **Consultant**: mianasghar124@gmail.com (PK property)

### PT Property Tax (Portugal IMI)
- **Drafter**: Meer or Amir
- **TO**: afeerasta@earthlink.net + apaamorais@gmail.com (Paula Morais, PT representative)
- **CC**: amfeerasta@gmail.com
- **Note**: emails in mix of English + reference to Paula's PT tax rep services

### GST / Sales Tax
- **Drafter**: Asif (28/50)
- **TO**: mfeerasta@rupafab.com + srzaidi5@gmail.com + afeerasta@earthlink.net
- **CC**: accounts.payable@rupafab.com (always)

### Court / Litigation
- **Drafter**: Asif (18/50) or Mustafa Law (mlawakeel@gmail.com)
- **TO**: afeerasta@earthlink.net + mfeerasta@rupafab.com (both Meer + Amir)
- **CC**: accounts.payable@rupafab.com
- **Subject prefix**: often `Lahore High Court Grants...`

### Markup (SBL)
- **Drafter**: Asif (currently — Hermes replacing from May 2026)
- **TO**: mfeerasta@rupafab.com (43/50)
- **CC**: accounts.payable@rupafab.com (40/50) + afeerasta@earthlink.net (19/50) + afeerasta@hhhc.com (18/50)
- **Subject prefix**: `PER-ACCT-`

### CDC Charges
- **Drafter**: Asif (when consolidating) — Hermes replacing
- **Asif sends TO**: afeerasta@earthlink.net (Amir, primary CDC holder)
- **Asif CCs**: mfeerasta@rupafab.com
- **Raw CDC stmts come TO**: amfeerasta@gmail.com + afeerasta@hhhc.com (Amir's mailboxes)

### Approvals (AP)
- **Drafter**: Ashar (accounts.payable) — 50/50
- **TO**: mfeerasta@rupafab.com (always)
- **CC**: asifh@rupafab.com + afeerasta@earthlink.net (always both)
- **Subject prefix**: `RFB-App-Tran-` (Rupafab) or `ZP-App-Tran-` (Zindar Property/personal)

### Daily Task Report
- **Drafter**: Asif (22/50) or Ashar (17/50) or AGRI mgr (agrinazir@)
- **TO**: mfeerasta@rupafab.com (always)
- **CC**: afeerasta@earthlink.net + asifh@ + accounts.payable@

### Salary / Bonus
- **Drafter**: Ashar (30/50) or Meer (20/50, approving)
- **TO**: mfeerasta@rupafab.com or accounts.payable@
- **CC**: afeerasta@earthlink.net + asifh@ (always both, every salary email)

### Family transfers (Ammi etc.)
- **Drafter**: Asif (22/50)
- **TO**: mfeerasta@rupafab.com + Soneri bank officer (chishti.ghulam@ or arslan.shehzad@soneribank.com)
- **CC**: accounts@rupafab.com + accounts.payable@ + afeerasta@earthlink.net

## Style conventions

- **Greeting**: `Dear Sir,` (FBR, govt, formal) | `Dear FD Sb,` (Asif → Meer, "Financial Director Saab") | `Dear Sir/ FD SB.` (markup emails)
- **Body**: short paragraphs, single-sentence bullets, lots of blank lines (Outlook style)
- **Sign-off (Asif's, replace with Hermes line)**:
  ```
  Regards,
  Hermes (AI agent for M. Feerasta)
  hermes@feerasta.pk
  ```
- **Subject prefix conventions**:
  - `PER-ACCT-` — personal accounts (markup, CDC, individual statements)
  - `RFB-ACCT-` — Rupafab Limited accounts/finance
  - `RFB-App-Tran-` — Rupafab approval-to-transact requests
  - `ZP-App-Tran-` — Zindar Property approval requests
  - `Rupafab Ltd.` — formal company correspondence (FBR replies, court)
  - `Rupafab Ltd:` — internal company memos (PESSI, GST, board)
  - `App-CashCK-` — cash check approval
  - `App-Cash-` — direct cash payment
  - `Daily Task Report-AH-` (Asif) / `-AS-` (Ashar) — daily reports

## When Hermes drafts emails

1. Look up category here to determine TO + CC list (do NOT invent recipients)
2. Match subject prefix (PER-ACCT-, RFB-ACCT-, etc.)
3. Greeting: pick from formal/informal column
4. Body: terse, Outlook-style spacing, end with `Regards,\nHermes ...`
5. Always auto-CC meerfeerasta@gmail.com via hermes_mailer (already wired)
6. Risk-band check: govt/court/tax → approval-gates risk_band=high; family transfers also high
7. Attachments: same Asif convention (xlsx + supporting PDFs)
