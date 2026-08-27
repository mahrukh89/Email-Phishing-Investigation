# Screenshots index

This folder holds the visual evidence for each analysis step. Capture and
name them exactly as below so they line up with the references in
`investigation/*.md` and the main `README.md`.

| File | What to capture |
|---|---|
| `01-email-header.png` | Full raw header block of `phishing_email.eml` opened in a text editor or email client |
| `02-authentication-results.png` | The `Authentication-Results` line (SPF/DKIM/DMARC) highlighted |
| `03-email-url.png` | The rendered email body with the malicious link visible/hovered |
| `04-url-analysis.png` | The link destination inspected (e.g. hovering to reveal `cloudora-hr-verify.example`, or a sandbox/URL analysis view) |
| `05-message-trace.png` | `cloudora_msgtrace_logs.csv` opened, sorted by `Status` |
| `06-click-analysis.png` | `cloudora_click_delivery_logs.csv` filtered to `Clicked = YES` |
| `07-signin-analysis.png` | `cloudora_entra_signin_logs.csv` filtered to the anomalous IP/location |
| `08-kql-correlation.png` | The KQL join query (from `kql/signin-investigation.kql`) and its result grid |
| `09-final-findings.png` | Your final summary view — timeline chart, dashboard, or findings table |

Keep these as clean crops (no unrelated desktop clutter) — this is the
part reviewers actually look at first.
