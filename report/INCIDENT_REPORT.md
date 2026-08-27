<div align="center">

# Incident Report — Cloudora Payroll Phishing Campaign

**Classification:** Simulated / Synthetic Training Incident
**Date of activity:** 24 August 2026
**Prepared by:** *(your name)*

</div>

> ⚠️ **Simulation Notice** — This is a fictional incident created for
> training and portfolio purposes. All organizations, users, domains, and
> IP addresses are synthetic. See the root [`README.md`](../README.md) for
> full details.

---

## 1. Executive summary

On 24 August 2026, a phishing email impersonating *Cloudora Payroll
Services* was sent to six employees, using a payroll-verification lure to
harvest credentials. One message was quarantined as spam; five were
delivered. Two recipients clicked the embedded link. Correlating click
telemetry with identity sign-in logs confirmed that **one account
(`employee03@cloudora.example`) was successfully compromised** via a
credential-phish, while a second account's takeover attempt was **blocked
by Conditional Access / MFA**.

| Metric | Value |
|---|---|
| Emails delivered | 5 / 6 |
| Recipients who clicked | 2 |
| Accounts compromised | 1 |
| Time to compromise (click → sign-in) | ~44 seconds |
| Detection method | Cross-source log correlation (email + identity) |

## 2. Scope

- **Client:** Cloudora (fictional)
- **Threat:** Credential-harvesting phishing campaign
- **Affected systems:** Microsoft 365 (Exchange Online, Entra ID)

## 3. Timeline

| Time (UTC) | Event |
|---|---|
| 09:38:41 | Phishing email delivered to 5 of 6 targets |
| 09:41:03 | `employee03` clicks the malicious link |
| 09:41:47 | `employee03` — successful sign-in from anomalous IP, **no MFA challenge** |
| 09:43:20 | `employee03` — second sign-in to Microsoft 365 Portal, same IP |
| 09:44:12 | `employee02` clicks the malicious link |
| 09:44:55 | `employee02` — sign-in attempt **blocked by MFA** |
| 09:50:02 | `employee03` — Exchange Online PowerShell access from same anomalous IP |
| 10:05:33 | `employee03` — legitimate sign-in resumes from normal Chicago IP |

📷 `../evidence/screenshots/09-final-findings.png` — final timeline / summary view

## 4. Indicators of compromise

| Type | Value |
|---|---|
| Sender domain | `cloudora-hr.example` |
| Sender IP | `203.0.113.44` |
| Phishing URL domain | `cloudora-hr-verify.example` |
| Attacker sign-in IP | `198.51.100.77` |
| Anomalous geolocation | Romania (vs. normal Chicago, US) |
| Compromised account | `employee03@cloudora.example` |

## 5. Root cause

Absence of enforced Multi-Factor Authentication allowed a single
successful credential-phish to translate directly into account takeover.
The identical attack against a second user was neutralized purely because
Conditional Access enforced an MFA challenge — the presence or absence of
one control was the entire difference between the two outcomes.

*(Expand this section with your own analysis — this is the part that
should read as your independent judgment, not a template.)*

## 6. Impact

One mailbox potentially exposed to unauthorized access, including
possible mail rule manipulation via subsequent PowerShell access. No
evidence in this dataset of lateral movement beyond the single account.

## 7. Remediation actions taken / recommended

1. **Disable** `employee03@cloudora.example` immediately; force password
   reset and revoke all active sessions/refresh tokens.
2. **Audit mailbox rules** on the compromised account for unauthorized
   forwarding or auto-delete rules created after 09:41 UTC.
3. **Block** the sender domain `cloudora-hr.example` and phishing domain
   `cloudora-hr-verify.example` at the email gateway and web proxy.
4. **Enforce MFA universally** — extend the Conditional Access coverage
   that protected `employee02` to close the gap that failed to protect
   `employee03`.
5. **Notify** all 5 delivered recipients and run a phishing-awareness
   refresher using this (labeled, synthetic) email as a case study.
6. **Hunt further:** review `employee03`'s mailbox for propagation and
   check for sign-ins to other apps from the same attacker IP.

## 8. Lessons learned

*(Write 3–5 sentences in your own words — what worked, what didn't, and
what you'd check first in a real incident of this type. This is the
section hiring managers read most closely.)*

## 9. References

- Full investigation notes: [`../investigation/`](../investigation/)
- Queries used: [`../kql/`](../kql/)
- ATT&CK mapping: [`../mitre/ATTACK_MAPPING.md`](../mitre/ATTACK_MAPPING.md)
