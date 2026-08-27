# Phase 3 — Threat intelligence

**Objective:** Consolidate all IOCs and describe how you would validate
them against real threat intelligence sources.

## Consolidated IOC list

| Type | Value | Confidence |
|---|---|---|
| Sender domain | `cloudora-hr.example` | High |
| Sender IP | `203.0.113.44` | High |
| Phishing landing domain | `cloudora-hr-verify.example` | High |
| Attacker/sign-in IP | `198.51.100.77` | High |
| Anomalous geolocation | Romania (vs. normal Chicago, US baseline) | Medium |
| Compromised account | `employee03@cloudora.example` | High |

> These IOCs are fictional (reserved documentation ranges/domains) — in a
> real investigation you would not find them in any live threat feed.

## How you'd validate these in a real environment

| Source | What you'd check |
|---|---|
| VirusTotal | Domain/IP reputation, related samples, passive DNS |
| urlscan.io | Screenshot + behavior of the landing page, redirect chain |
| AbuseIPDB | Prior abuse reports against the sign-in IP |
| Microsoft Defender / Sentinel TI | Whether the domain/IP is already flagged internally |
| WHOIS / domain age | Newly registered lookalike domains are a strong signal |

## Analyst note

*(Describe what you'd do if one of these IOCs came back as "unknown" —
i.e., no prior reputation. Would that change your confidence in the
verdict? Why or why not?)*

Continue to [`campaign-scoping.md`](campaign-scoping.md).
