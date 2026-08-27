# Phase 4 — Campaign scoping

**Artifacts:** `evidence/cloudora_msgtrace_logs.csv`, `evidence/cloudora_click_delivery_logs.csv`
**Query used:** [`kql/message-trace.kql`](../kql/message-trace.kql), [`kql/click-investigation.kql`](../kql/click-investigation.kql)

## Objective

Establish the full blast radius: who received the email, and who engaged
with it.

## Delivery scope

| Recipient | Status |
|---|---|
| employee01@cloudora.example | Delivered |
| employee02@cloudora.example | Delivered |
| employee03@cloudora.example | Delivered |
| employee04@cloudora.example | Delivered |
| employee05@cloudora.example | Delivered |
| employee06@cloudora.example | Filtered as spam |

📷 `evidence/screenshots/05-message-trace.png` — message trace sorted by status

- **Recipients targeted:** 6
- **Delivered:** 5
- **Filtered:** 1
- **Common source IP across all messages:** `203.0.113.44` — confirms this
  was a single-source campaign, not multiple attackers.

## Click engagement

| Recipient | Clicked | Click time (UTC) | Source IP |
|---|---|---|---|
| employee02@cloudora.example | Yes | 09:44:12 | 198.51.100.77 |
| employee03@cloudora.example | Yes | 09:41:03 | 198.51.100.77 |
| employee01, 04, 05 | No | — | — |

📷 `evidence/screenshots/06-click-analysis.png` — click/delivery log filtered to `Clicked = YES`

## Analyst note

*(2/5 delivered recipients clicked — a 40% click rate. Is that high or low
compared to typical phishing simulation benchmarks you're aware of? What
would you recommend based on that number alone?)*

Continue to [`sign-in-investigation.md`](sign-in-investigation.md).
