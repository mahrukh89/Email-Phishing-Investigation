# MITRE ATT&CK mapping

Mapping the observed activity to MITRE ATT&CK (Enterprise) techniques.
This is what turns a narrative writeup into something a SOC/CTI reader can
immediately slot into their own framework.

| Stage | Technique | ID | Evidence |
|---|---|---|---|
| Initial Access | Phishing: Spearphishing Link | T1566.002 | `evidence/phishing_email.eml` — malicious link delivered via email |
| Initial Access | Valid Accounts | T1078 | Attacker authenticated with `employee03`'s legitimate, harvested credentials |
| Credential Access | Input Capture (via fake login portal) | T1056 (conceptual — landing page not included in this pack) | `cloudora-hr-verify.example/portal/login` lure page |
| Defense Evasion | (Domain) Masquerading | T1036.005 | Lookalike domain `cloudora-hr.example` impersonating `cloudora.example` |
| Persistence (suspected — recommend hunting) | Email Forwarding Rule | T1114.003 | Not directly evidenced in this dataset — flagged as a hunt priority given PowerShell access |
| Execution / Collection | Exchange Online PowerShell access | T1059 / T1114 | `evidence/cloudora_entra_signin_logs.csv` — `AppDisplayName = Exchange Online PowerShell` shortly after compromise |
| Discovery | Impossible travel / anomalous geolocation | N/A (detection pattern, not an attacker technique) | Sign-in from Romania vs. normal Chicago baseline |

## Why MFA mattered here (ATT&CK mitigation)

**Mitigation M1032 — Multi-factor Authentication** directly explains the
difference in outcome between the two clickers in this case:

- `employee02` — MFA challenge enforced → takeover **blocked**
- `employee03` — no MFA challenge recorded → takeover **succeeded**

## Recommended detections to build from this case

- Alert on sign-ins where `ConditionalAccessStatus` is not `mfaRequired`
  **and** the geolocation deviates from the user's historical baseline.
- Alert on `Exchange Online PowerShell` sessions immediately following an
  anomalous-location sign-in.
- Alert on new mailbox inbox rules created within 30 minutes of an
  anomalous sign-in (hunt priority noted above).
