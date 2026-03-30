---
name: top-20-accounts-scan
description: Health Scan of Top 20 Accounts
---


# Top 20 Account Intelligence System — Daily Scan

## FIXED ACCOUNT LIST (never change these)
Business IDs: 19127, 14132, 11866, 29115, 17014, 27750, 27890, 19934, 26836, 34511, 29930, 29530, 36644, 30254, 14350, 27862, 28447, 35941, 21977, 26187

## OUTPUT FILES (persist all data to these paths)
- Hex raw data: `/sessions/funny-kind-pasteur/mnt/outputs/account_intelligence/hex_raw_{DATE}.md`
- Enrichment data: `/sessions/funny-kind-pasteur/mnt/outputs/account_intelligence/enrichment_{DATE}.md`
- Where `{DATE}` = today's date in YYYY-MM-DD format

---

## STEP 1 — HEX FINANCIAL SIGNALS

Query the following 6 signals via Hex for all 20 BIDs. Run queries in parallel where possible.

1. **Deposit Movements** — 30-day balance change ($, %) per account
2. **Card Spend Velocity** — 30-day card authorization count and volume, vs. prior 30 days
3. **Balance Decline + Credit Utilization** — current balance, credit limit, utilization %
4. **Product Adoption & Dormancy** — which products are active (Cards, AP, Expense, Checking, Treasury), days since last activity per product
5. **Wallet Share** — % of estimated spend going through Rho cards
6. **Fundraise Radar** — any large inflows ($500K+) in last 30 days, counterparty names

Write ALL raw results to `hex_raw_{DATE}.md` before proceeding. Do not move to Step 2 until this file is written.

---

## STEP 2 — DEEP ENRICHMENT (MANDATORY — NO SHORTCUTS)

### CORE RULE: Every account. Every source. Every time.

For EVERY one of the 20 accounts, you MUST query ALL of the following sources. A single search that returns sparse results does NOT satisfy the requirement — you must try multiple query variants before concluding that no intel exists on a source.

---

### SOURCE 1: SLACK (minimum 3 query variants per account)
You must run at least 3 separate Slack searches per account using different query formulations:
- Query A: `"{legal name}" {BID}` — exact name + ID
- Query B: `"{short name or common abbreviation}"` — how the team refers to them informally
- Query C: Targeted signal search: `"{name}" issue OR error OR escalat OR urgent OR churn OR cancel OR risk`
- Query D (if A-C return thin results): `"{name}" card OR treasury OR wire OR payment OR onboarding`

For each account, also search these specific channels if the above return nothing useful:
- `#cs-asap-support in:{name}`
- `#transaction-slo {BID}`
- `#ach-returns-monitoring {BID}`
- `#cs-churn-and-upsell-alerts {BID}`

**DO NOT accept a single failed or thin search as "no Slack activity." Try all variants. Only write "no Slack intel found" after running a minimum of 3 query variants that all return nothing relevant.**

---

### SOURCE 2: GMAIL
Search Gmail for each account using:
- Query A: `from:{company domain} OR to:{company domain}` — direct email correspondence
- Query B: `"{legal name}" subject:` — account name in subject lines
- Query C: `"{name}" (invoice OR payment OR issue OR renewal OR concern)`

Look for: recent direct correspondence, support emails, any communication in last 90 days. Note last email date, who sent it, what it was about.

---

### SOURCE 3: GRANOLA (meeting notes)
Query Granola for each account:
- Search by company name
- Search by key contact names if known
- Look back 90 days minimum

Capture: last meeting date, attendees, key discussion topics, ANY action items that are open/pending.

---

### SOURCE 4: CALENDAR
Check upcoming calendar events for each account:
- Search by company name
- Search by known contact names
- Flag any meetings in the next 14 days

---

### SOURCE 5: HARMONIC
For accounts flagged as ACTION or MONITOR tier, query Harmonic for:
- Recent funding rounds (last 6 months)
- Headcount changes (growth or contraction)
- Company description and stage
- Any news signals

This adds critical external business context to internal financial signals.

---

### SOURCE 6: NOTION / CONFLUENCE / JIRA
Search for any internal documentation, project notes, or support tickets related to the account:
- Account strategy docs
- Open Jira tickets or escalations
- Any playbooks or notes from CS team

---

### ENRICHMENT QUALITY STANDARD
Before writing any account's enrichment to the file, ask yourself:
1. Did I run at least 3 Slack variants for this account?
2. Did I search Gmail?
3. Did I search Granola?
4. Did I check Calendar?
5. For ACTION/MONITOR accounts: Did I query Harmonic?

If the answer to any of these is NO — go back and run those searches before writing. No exceptions.

When you write enrichment for an account, use this format:
```
### {BID} — {Name}
**Hex Signal:** [summary of financial signals]
**Slack:** [findings from all variants searched, or "Searched 4 variants — no relevant intel found"]
**Gmail:** [last correspondence date, subject, who sent it — or "No correspondence found in last 90 days"]
**Granola:** [last meeting date, key topics, open action items — or "No meetings found"]
**Calendar:** [upcoming meetings — or "None scheduled"]
**Harmonic:** [funding stage, recent news, headcount trend — or "Not queried (STABLE tier)"]
**Narrative:** [2-3 sentence synthesis connecting the signals: what is the STORY of this account right now?]
**Specific Action:** [exact conversation hook — not "call them" but what to say, what to ask, what timing angle to use]
```

Write ALL 20 accounts to `enrichment_{DATE}.md` before proceeding to Step 3.

---

## STEP 3 — RECONCILIATION

Read both the `hex_raw` and `enrichment` files in full. Apply these rules:

**Escalate to ACTION if:**
- Balance decline >3% AND no recent positive engagement signal in any source
- Any product dormant >90 days AND no meeting or email in last 45 days
- Card spend decline >50% with no external explanation
- Any open escalation or unresolved support issue in Slack/Jira

**Downgrade from ACTION to MONITOR if:**
- Hex shows negative signal BUT Granola/Gmail/Slack shows active engagement in last 30 days
- Decline is explained by a known event (fundraise deployment, seasonal, etc.)

**Escalate to EXPANSION if:**
- Inflow >$500K with identifiable fundraise source
- Card spend increase >100% sustained over 2+ weeks
- Recently migrated from competitor (Mercury, Brex, Ramp) — confirmed in Slack/Granola

**Conflict resolution:** Contextual signal (recent meeting, active email thread) always overrides raw financial signal in tier assignment. Financial signal sets the flag; context determines the urgency and action.

---

## STEP 4 — COMPOSE THE BRIEF

### MANDATORY BRIEF STANDARD

Every ACTION account entry MUST contain:

1. **Signal** — the specific Hex metric and its magnitude
2. **Business Context** — what is this company doing right now? (stage, product, recent news)
3. **Relationship Status** — last touchpoint date, channel, who was involved
4. **Risk Narrative** — the specific mechanism of risk: WHY does this signal matter for THIS account?
5. **Conversation Hook** — the exact angle for outreach: what to open with, what question to ask, what timing to reference
6. **What Success Looks Like** — what outcome are you driving toward in this interaction?

Entries without ALL 6 components are incomplete. Do not include incomplete entries in the brief.

For MONITOR accounts: minimum Signal + Relationship Status + Watch Trigger (what specific change would move this to ACTION).

For EXPANSION accounts: minimum Signal + Business Context + Specific Opportunity + Timing Rationale.

### BRIEF FORMAT

```
# Top 20 Account Intelligence Brief — {DATE}
Generated: {time}

## 🔴 ACTION ({N} accounts)
[Full 6-component entries]

## 🟡 MONITOR ({N} accounts)
[Condensed entries]

## 🟢 EXPANSION ({N} accounts)
[Opportunity-framed entries]

## ⚪ STABLE ({N} accounts)
[One-liner table]

## Portfolio Health Snapshot
[Aggregate metrics]

## Today's Priority Queue
[Top 3-5 actions ranked by urgency × impact]
```

---

## STEP 5 — DELIVER

1. Create a Slack Canvas with the full brief (title: "Top 20 Account Intelligence Brief — {DATE}")
2. Send a DM to Yonas (user_id: U09SGCDPJKD) with:
   - 🔴 count and top 2 ACTION accounts (1-line each)
   - 🟢 top expansion opportunity (1-line)
   - Direct link to the Canvas

---

## EXECUTION PRINCIPLES

- **Never accept thin enrichment.** If a source returns nothing, try different query variants before writing "no intel found."
- **Quantity of searches ≠ quality of synthesis.** Run many searches, but synthesize concisely and specifically.
- **Specificity is the standard.** "Call them" is not an action. "Open with the March wire inquiry and ask about their new funding use case" is an action.
- **Flag intelligence gaps honestly.** If you genuinely searched 4+ variants across 3+ sources and found nothing, write: "⚠️ No enrichment found after exhaustive search — treat as unknown relationship status."
- **Persist data at every step.** Write to files after Step 1 and after Step 2. Never hold data only in memory across a long enrichment loop.
