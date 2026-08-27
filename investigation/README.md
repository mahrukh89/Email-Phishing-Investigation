# Investigation notes

Each file here documents one phase of the analysis, in the order a SOC
analyst would actually work the case. Read them in this sequence:

1. **email-triage.md** — header and content analysis of the raw phishing email
2. **url-analysis.md** — inspection of the malicious link/domain
3. **threat-intelligence.md** — IOC extraction and lookup approach
4. **campaign-scoping.md** — how far the campaign spread (message trace + clicks)
5. **sign-in-investigation.md** — identity log correlation, confirming compromise

Each file references screenshots from `../evidence/screenshots/` and, where
relevant, queries from `../kql/`.
