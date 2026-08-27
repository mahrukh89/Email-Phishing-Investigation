<div align="center">

# 🛡️ Cloudora Phishing Incident Investigation
### A Simulated SOC Analyst Investigation — Email Forensics, Log Correlation, KQL & MITRE ATT&CK Mapping

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Type](https://img.shields.io/badge/type-synthetic%20lab-blue)
![Focus](https://img.shields.io/badge/focus-SOC%20%7C%20Phishing%20%7C%20KQL-orange)
![Data](https://img.shields.io/badge/data-fictional-lightgrey)

</div>

> **⚠️ Simulation Notice**
> This repository documents a **fully synthetic security incident**
> created for training and portfolio purposes. The organization
> ("Cloudora"), employees, domains, IP addresses, and email content are
> **entirely fictional**. Domains use the `.example` TLD (reserved for
> documentation under RFC 2606) and IPs use TEST-NET ranges
> (`192.0.2.0/24`, `198.51.100.0/24`, `203.0.113.0/24`) reserved for
> documentation use. No real organization, person, or system was involved.

---

## 📌 Executive summary

A phishing email impersonating *Cloudora Payroll Services* was sent to six
employees. Two clicked the embedded credential-harvesting link.
Correlating email telemetry with identity sign-in logs confirmed **one
account was fully compromised**, while a second account's takeover attempt
was **blocked by MFA** — the single control that made the difference.
Full findings are in [`report/INCIDENT_REPORT.md`](report/INCIDENT_REPORT.md).

| Metric | Value |
|---|---|
| Emails delivered | 5 / 6 |
| Recipients who clicked | 2 |
| Accounts compromised | 1 |
| Detection method | Cross-source log correlation (email + identity) |

## 🗂️ Repository structure

```
Cloudora-Phishing-Investigation/
│
├── README.md                      <- you are here
│
├── evidence/                      <- raw artifacts
│   ├── phishing_email.eml
│   ├── cloudora_msgtrace_logs.csv
│   ├── cloudora_click_delivery_logs.csv
│   ├── cloudora_entra_signin_logs.csv
│   │
│   └── screenshots/                <- visual evidence per analysis step
│       ├── README.md                 (index of what each screenshot shows)
│       ├── 01-email-header.png
│       ├── 02-authentication-results.png
│       ├── 03-email-url.png
│       ├── 04-url-analysis.png
│       ├── 05-message-trace.png
│       ├── 06-click-analysis.png
│       ├── 07-signin-analysis.png
│       ├── 08-kql-correlation.png
│       └── 09-final-findings.png
│
├── investigation/                 <- step-by-step analyst writeup
│   ├── README.md                    (reading order)
│   ├── email-triage.md
│   ├── url-analysis.md
│   ├── threat-intelligence.md
│   ├── campaign-scoping.md
│   └── sign-in-investigation.md
│
├── kql/                            <- queries used for correlation
│   ├── README.md                    (table import guide)
│   ├── message-trace.kql
│   ├── click-investigation.kql
│   └── signin-investigation.kql
│
├── mitre/
│   └── ATTACK_MAPPING.md           <- MITRE ATT&CK technique mapping
│
└── report/
    └── INCIDENT_REPORT.md          <- final polished incident report
```

## 🧭 How to read this repo

1. Start with this README for the overview.
2. Walk through [`investigation/`](investigation/) in order — it mirrors
   the actual analyst workflow, phase by phase, with embedded screenshots.
3. Check [`kql/`](kql/) for the exact queries used to correlate the data.
4. See [`mitre/ATTACK_MAPPING.md`](mitre/ATTACK_MAPPING.md) for how the
   activity maps to MITRE ATT&CK techniques.
5. Read [`report/INCIDENT_REPORT.md`](report/INCIDENT_REPORT.md) for the
   final, polished incident report — the deliverable a real SOC would
   produce.

## 🧰 Tools & skills demonstrated

| Category | Tool / technique |
|---|---|
| Email forensics | Manual `.eml` / header analysis (SPF, DKIM, DMARC) |
| Log analysis | Mail trace, click telemetry, identity sign-in logs |
| Query language | KQL (Kusto Query Language) via Azure Data Explorer |
| Correlation | Cross-referencing timestamps across 3 independent data sources |
| Threat intel | IOC extraction and validation methodology |
| Threat modeling | MITRE ATT&CK technique mapping |
| Documentation | Structured Markdown incident reporting |

## 🔁 Reproducing / customizing this lab

`generate_dataset.py` regenerates the three evidence CSVs — edit the
constants at the top (which account gets compromised, employee count,
timestamps) and rerun it to build your own variant of this scenario.

---

<div align="center">

*Built as a self-directed synthetic SOC lab to practice phishing triage,
log correlation, KQL, and ATT&CK mapping — independently reconstructed
with original synthetic data.*

</div>
