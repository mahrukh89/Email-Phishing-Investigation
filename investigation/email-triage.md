# Phase 1 — Email triage

**Artifact:** `evidence/phishing_email.eml`

## Objective

Determine whether the email is authentic and extract the initial
indicators of compromise (IOCs).

## Header analysis

| Header | Value | Assessment |
|---|---|---|
| `From` | `payroll@cloudora-hr.example` | Impersonates a payroll department |
| `Return-Path` | `bounce@cloudora-hr.example` | Consistent with the *lookalike* domain, not the real `cloudora.example` |
| `Received` | via `mail-relay-09.cloudora-hr.example` (`203.0.113.44`) | External relay, not an internal Cloudora mail server |
| `SPF` | `softfail` | Sending IP not authorized for the claimed domain |
| `DKIM` | `fail` | Signature does not validate |
| `DMARC` | `fail`, policy `p=none` | Failures logged but **not enforced** — this is why the message reached the inbox at all |

📷 `evidence/screenshots/01-email-header.png` — full header block
📷 `evidence/screenshots/02-authentication-results.png` — SPF/DKIM/DMARC line highlighted

## Content analysis

- **Urgency lure:** "expires at 5:00 PM today" — classic pressure tactic to
  short-circuit careful review.
- **Generic salutation:** "Dear Employee" rather than a named greeting —
  suggests a bulk send rather than a targeted spear-phish.
- **Mismatched branding:** claims to be Cloudora Payroll but the sending
  domain (`cloudora-hr.example`) does not match the organization's real
  domain (`cloudora.example`).

## Analyst note

*(Write 2-3 sentences here in your own words: why would this specific
email deceive a typical employee, and which single artifact — header or
content — was the clearest giveaway to you?)*

## IOCs extracted at this phase

| Type | Value |
|---|---|
| Sender domain | `cloudora-hr.example` |
| Sender IP | `203.0.113.44` |
| Message-ID | `9f3c1a2e-4b7d-4e21-9a0c-2d5f6b8e7a11@cloudora-hr.example` |

Continue to [`url-analysis.md`](url-analysis.md).
