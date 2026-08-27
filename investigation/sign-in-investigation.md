# Phase 5 — Sign-in investigation & correlation

**Artifact:** `evidence/cloudora_entra_signin_logs.csv`
**Query used:** [`kql/signin-investigation.kql`](../kql/signin-investigation.kql)

## Objective

Determine whether either click led to an actual account compromise.

📷 `evidence/screenshots/07-signin-analysis.png` — sign-in log filtered to the anomalous IP/location
📷 `evidence/screenshots/08-kql-correlation.png` — KQL join query + result grid

## Correlated result

| User | Click time | Sign-in time | Location | MFA status | Outcome |
|---|---|---|---|---|---|
| employee03 | 09:41:03 | 09:41:47 | Romania (anomalous) | Not enforced | **Compromised** |
| employee02 | 09:44:12 | 09:44:55 | Romania (anomalous) | MFA challenge failed | Blocked — not compromised |

## Follow-on activity (employee03 only)

| Time (UTC) | Event |
|---|---|
| 09:43:20 | Second sign-in to Microsoft 365 Portal, same anomalous IP |
| 09:50:02 | Access via **Exchange Online PowerShell**, same anomalous IP |
| 10:05:33 | Legitimate sign-in resumes from normal Chicago IP |

`Exchange Online PowerShell` access shortly after compromise is notable —
it's a common mechanism attackers use to create hidden **mailbox
forwarding or inbox rules** for persistent access after credentials are
stolen.

## Analyst note

*(Write your conclusion here: why did employee02's compromise attempt fail
where employee03's succeeded, and what single control made the
difference? This is your core finding — make it explicit.)*

Continue to the final [`report/INCIDENT_REPORT.md`](../report/INCIDENT_REPORT.md)
and the [`mitre/ATTACK_MAPPING.md`](../mitre/ATTACK_MAPPING.md).
