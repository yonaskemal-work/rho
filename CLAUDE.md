# Yonas Kemal — AM Intelligence Context

This file is loaded automatically in every Claude Code session. It provides standing context about Yonas's role, book of business, quota, tools, and working preferences. All skills and workflows should reference this as ground truth.

---

## Identity

- **Name:** Yonas Kemal
- **Role:** Account Manager, Rho
- **Email:** yonas.kemal@rho.co
- **Slack User ID:** U09SGCDPJKD
- **Manager:** Stephanie
- **Director:** J.D.

---

## The Company

Rho is a business banking platform for startups. Core revenue comes from:
- **Deposit yield** — interest earned on checking, savings, and treasury balances
- **Interchange** — revenue from card swipes

Customers are mostly VC-backed startups, with some CPG companies and SMBs. Accounts tend to be founder-led early-stage companies, though some are older and more established.

---

## Book of Business

- **Size:** ~400–450 accounts
- **Primary contacts:** typically the founder, CFO, controller, outsourced accounting team, or an ops/finance hire
- **Segmentation:** Based on GP/deposit size + hard-coded logic for YC-backed and top VC-backed companies. Segmentation is being revised — updated logic will be reflected in Salesforce soon. Do not rely on current Salesforce segmentation tiers as final.
- **Growth AE assignment:** Each account is assigned either Brendan Feehan or Abigail Geyser. Assignment lives in Salesforce.

---

## Rho Product Lines

These are the products that count toward feature adoption quota:

| Product | Category |
|---|---|
| Checking | Cash Management Suite |
| Savings | Cash Management Suite |
| Treasury | Cash Management Suite |
| Cards | Card / Expense Management |
| Expense Management | Card / Expense Management |
| AP / Bill Pay | Accounts Payable |

An account "adopts" a feature when they activate and use a product they weren't previously using. Multiple adoptions per account count. Accounting integrations are excluded from quota tracking.

---

## Q2 2026 Quota Structure

**Split:** 50% Retention / 25% Upsell Approvals / 25% Feature Adoption

### 1. Team Retention (50%)
- Team book of business GP locked on **April 10** (10 days after EOQ)
- Retention = GP retained at quarter end ÷ locked GP at quarter start
- Payout scale:
  - 90–100% retention → 100% payout (capped)
  - 80–89% → 1:1 payout
  - <80% → no payout
- This is a **team metric** — individual AMs don't control it directly. Historically never below 90%. Treat as near-certain.

### 2. Upsell Approvals (25%)
- **Target:** 8 per quarter
- **Process:** Identify an account with expansion opportunity (money elsewhere, upcoming raise, underutilized products) → submit via Salesforce → growth AE (Brendan or Abigail) approves
- **Carry forward:** Unused approvals carry into Q3
- **Signals to look for:** funds held at other banks, upcoming fundraise, deposits growing, low wallet share, strong relationship with no product depth

### 3. Feature Adoption (25%)
- **Target:** 45 per quarter
- **Tracked by:** Stephanie and J.D. Raw data in Snowflake, synced to Salesforce
- **Carry forward:** Unused adoptions carry into Q3
- **Counts:** Any account activating a net-new product line
- **Strategy:** Surface accounts with product gaps who show engagement signals — don't just look at what's missing, look at what's been mentioned in conversations or emails

### Attainment Formula
```
Total = (50% × Retention%) + (25% × Upsell Attainment%) + (25% × Feature Attainment%)
```
- Total attainment capped at 200%
- Example: 100% retention + 150% upsell + 88% feature = 109.5% payout

---

## Data Sources & Where Things Live

| Source | What's There |
|---|---|
| **Salesforce** | Account records, product usage (synced from Snowflake), growth AE assignment, upsell submission button, money elsewhere field (TBD — verify field name), activities/notes |
| **Hex** | Financial signals: balance trends, card spend velocity, product dormancy, wallet share, large inflows |
| **Snowflake** | Raw data warehouse — source of truth for feature adoption (accessed via Hex or Salesforce sync) |
| **Slack** | Internal team comms, support escalations, CS alerts |
| **Gmail** | External client communication |
| **Granola** | Meeting notes and action items |
| **Google Calendar** | Upcoming meetings, last touchpoint scheduling |
| **Notion** | Internal docs, BoB pages, AM notes |
| **Jira** | Support tickets, escalations |
| **Harmonic** | Excluded — skip entirely in all workflows |

---

## Growth Account Executives

- **Brendan Feehan** — growth AE, assigned to subset of Yonas's accounts
- **Abigail Geyser** — growth AE, assigned to remaining accounts
- Upsell opportunities are flagged to the relevant AE and submitted via Salesforce for approval

---

## Working Style & Goals

- **Role of Claude:** Intelligent co-pilot. Handle the manual aggregation and synthesis of data across tools so Yonas can focus on human-to-human relationship work and decision-making.
- **Output standard:** Specificity is required. "Call them" is not an action. "Open with the March wire conversation and ask about their Series B timeline" is an action.
- **Don't ask for permission** within defined workflows. Execute fully and report back.
- **Draft outreach:** Surface drafts for review — do not send without explicit instruction.
- **Volume:** Prioritized shortlists (10–15 accounts) are more useful than exhaustive lists of 400.
- **Bigger goal:** Build systems and playbooks that Yonas can share with the AM team. Everything we build should be translatable into team-level documentation. This is how Yonas earns leadership leverage.

---

## Open Items (update as resolved)

- [ ] Confirm Salesforce field name for "money elsewhere" / external deposits
- [ ] Receive updated account segmentation logic when Salesforce is cleaned up
- [ ] Confirm which accounts are assigned to Brendan vs. Abigail in Salesforce
