# Cloudora Phishing Investigation

An end-to-end simulated phishing incident investigation built around a fictional organization, **Cloudora**. This project walks through the full lifecycle of a security incident response engagement — from initial email triage through threat intelligence enrichment, log analysis, campaign scoping, and final reporting — using realistic (synthetic) evidence and Microsoft 365 / Entra-style log data.

The goal of this repository is to demonstrate a structured, defensible SOC/IR investigation workflow, including hands-on KQL queries, MITRE ATT&CK mapping, and a polished incident report suitable for stakeholder review.

---

## 📁 Repository Structure

```
Cloudora-Phishing-Investigation/
│
├── README.md                          # This file
│
├── evidence/                          # Raw and collected evidence
│   ├── phishing_email.eml
│   ├── cloudora_msgtrace_logs.csv
│   ├── cloudora_click_delivery_logs.csv
│   ├── cloudora_entra_signin_logs.csv
│   │
│   └── screenshots/                   # Visual evidence from each investigation phase
│       ├── README.md
│       ├── 01-email-triage.png
│       ├── 02-header-analysis.png
│       ├── 03-url-analysis.png
│       ├── 04-threat-intelligence.png
│       ├── 05-message-trace.png
│       ├── 06-click-analysis.png
│       ├── 07-signin-analysis.png
│       ├── 08-campaign-correlation.png
│       └── 09-final-findings.png
│
├── investigation/                     # Written analysis for each investigation phase
│   ├── README.md
│   ├── email-triage.md
│   ├── url-analysis.md
│   ├── threat-intelligence.md
│   ├── campaign-scoping.md
│   └── sign-in-investigation.md
│
├── kql/                                # KQL queries used for log analysis (Sentinel/Defender-style)
│   ├── README.md
│   ├── message-trace.kql
│   ├── click-investigation.kql
│   └── signin-investigation.kql
│
├── mitre/
│   └── ATTACK_MAPPING.md              # MITRE ATT&CK technique mapping for the incident
│
├── report/
│   └── INCIDENT_REPORT.md             # Final consolidated incident report
│
├── architecture/
│   ├── README.md
│   └── ARCHITECTURE.md                # Environment/architecture overview for the simulated org
│
├── generate_dataset.py                # Script used to generate the synthetic log datasets
├── .gitignore
└── LICENSE
```

---

## 🎯 Project Objectives

- Simulate a realistic phishing incident against a fictional organization (Cloudora)
- Demonstrate a full IR workflow: triage → header analysis → URL/threat intel → log correlation → campaign scoping → reporting
- Practice writing and using KQL queries against message trace, click/delivery, and sign-in logs
- Map observed adversary behavior to the MITRE ATT&CK framework
- Produce a professional, stakeholder-ready incident report

---

## 🔍 Investigation Workflow

1. **Email Triage** — Initial assessment of the suspicious email and its headers
2. **Header Analysis** — Authentication results (SPF/DKIM/DMARC), routing, and sender legitimacy
3. **URL Analysis** — Inspection of embedded links, redirects, and landing pages
4. **Threat Intelligence** — Enrichment using OSINT/threat intel sources
5. **Message Trace** — Reviewing Cloudora's mail flow logs for delivery scope
6. **Click Analysis** — Determining who clicked the malicious link and when
7. **Sign-In Investigation** — Reviewing Entra ID sign-in logs for signs of compromise
8. **Campaign Correlation** — Identifying whether this was part of a broader campaign
9. **Final Findings** — Summary of scope, impact, and recommended remediation

Each phase has a corresponding write-up in [`investigation/`](investigation/) and supporting evidence in [`evidence/`](evidence/).

---

## 🧰 Tools & Techniques Used

- KQL (Kusto Query Language) for Microsoft Sentinel / Defender-style log analysis
- Email header and authentication analysis (SPF, DKIM, DMARC)
- URL/domain reputation and threat intelligence lookups
- Entra ID sign-in log review
- MITRE ATT&CK technique mapping
- Synthetic dataset generation via Python (`generate_dataset.py`)

---

## 📄 Key Documents

| Document | Description |
|---|---|
| [`report/INCIDENT_REPORT.md`](report/INCIDENT_REPORT.md) | Final consolidated incident report |
| [`mitre/ATTACK_MAPPING.md`](mitre/ATTACK_MAPPING.md) | MITRE ATT&CK technique mapping |
| [`architecture/ARCHITECTURE.md`](architecture/ARCHITECTURE.md) | Simulated environment/architecture overview |
| [`investigation/`](investigation/) | Phase-by-phase investigation notes |
| [`kql/`](kql/) | KQL queries used during the investigation |

---

## ⚠️ Disclaimer

This project is a **simulated, educational exercise**. "Cloudora" is a fictional organization, and all evidence, logs, and datasets included in this repository are **synthetically generated** for training and portfolio purposes. No real individuals, companies, or systems were involved.

---

## 📜 License

This project is licensed under the terms of the [LICENSE](LICENSE) file included in this repository.
