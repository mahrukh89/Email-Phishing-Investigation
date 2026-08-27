# Phase 2 — URL analysis

**Artifact:** the "Review Payroll Details" link inside `evidence/phishing_email.eml`

## Objective

Confirm whether the embedded link is malicious and understand what it was
built to do.

## Findings

| Element | Value |
|---|---|
| Displayed link text | "Review Payroll Details" |
| Actual destination | `https://cloudora-hr-verify.example/portal/login?ref=9f3c1a2e` |
| Domain | `cloudora-hr-verify.example` — a lookalike of the sender's already-spoofed domain, **not** the real Cloudora domain |
| URL path | `/portal/login` — designed to visually resemble a legitimate SSO/portal login page |
| Query parameter | `ref=9f3c1a2e` — matches the email's Message-ID, almost certainly used to tag which recipient clicked (click-tracking for the attacker, not for defenders) |

📷 `evidence/screenshots/03-email-url.png` — rendered email with the link visible/hovered
📷 `evidence/screenshots/04-url-analysis.png` — link destination inspection (hover-preview or sandbox/URL-analysis tool output)

## Why this matters

The `ref` parameter is the mechanism that connects an individual click back
to a specific recipient — this is exactly what shows up later as
`ClickSourceIP` / `ClickTimestamp` in `evidence/cloudora_click_delivery_logs.csv`.

## Analyst note

*(In your own words: what specific visual or structural cue in the URL
would you point to as the giveaway, and how would you explain it to a
non-technical employee?)*

Continue to [`threat-intelligence.md`](threat-intelligence.md).
